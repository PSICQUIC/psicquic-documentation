

## Purpose ##

This document focuses on several aspects of the [MITAB27 data representation](http://code.google.com/p/psicquic/wiki/MITAB27Format) in the context of data distribution via PSICQUIC services. As MITAB 2.7 is backward compatible with MITAB 2.5 and MITAB 2.6, the best practices also apply to these formats except for the new columns. The implementation of these best practices in the data served by a PSICQUIC services should improve users searches, data consistency and visualization as well as clustering of this data with other PSICQUIC services.


## Best Practices ##

### A. Describing an Interacting Molecule ###

Typically, an interacting molecule is described using up to 12 columns of the [MITAB format](http://code.google.com/p/psicquic/wiki/MITAB27Format):

| **Column name** | **Columns for Interactor A** | **Columns for Interactor B** | **Definition** |
|:----------------|:-----------------------------|:-----------------------------|:---------------|
| Unique identifier | 1 | 2 | represented as **databaseName:ac**, where databaseName is the name of the corresponding database as defined in the [PSI-MI controlled vocabulary](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MI&termId=MI:0444&termName=database%20citation), and ac is the unique primary identifier of the molecule in the database. Even though the MITAB format can accept several identifiers from multiple databases (separated by "&#124;") in the 'unique identifier' columns, it is recommended to give only one identifier. It is also recommended that proteins are identified by stable identifiers such as their UniProtKB, RefSeq, Ensembl, ddbj/genbank/embl or Chebi accession number.|
| Alternative Identifier | 3 | 4 | represented as **databaseName:ac**, where databaseName is the name of the corresponding database as defined in the [PSI-MI controlled vocabulary](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MI&termId=MI:0444&termName=database%20citation), and ac is the primary identifier of the molecule in the database. Multiple identifiers separated by "&#124;". It is recommended that only database identifiers for the interactors are given in these columns. Other cross references for these interactors such as GO xrefs should be moved to columns 23 and 24 and interactor names such as gene names should be moved to columns 5 and 6. |
| Aliases | 5 | 6 | represented as databaseName:name, where databaseName is the name of the corresponding database as defined in the [PSI-MI controlled vocabulary](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MI&termId=MI:0444&termName=database%20citation), and name is the name of the molecule in the database (Ex gene names, protein recommended name, ORF, locus name, drug name, Chebi recommended name, etc.). Multiple names separated by "&#124;".  |
| Xrefs | 23 | 24 | represented as **databaseName:ac**, where databaseName is the name of the corresponding database as defined in the [PSI-MI controlled vocabulary](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MI&termId=MI:0444&termName=database%20citation), and ac is the primary accession in the database. Multiple accessions separated by "&#124;". This columns can contain for instance GO xrefs. |
| NCBI Taxonomy identifier | 10 | 11 | Database name for NCBI taxid taken from the [PSI-MI controlled vocabulary](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MI&termId=MI:0444&termName=database%20citation), represented as **taxid:identifier(organism common name)**. Even though the MITAB format can accept several taxon ids per column (Multiple identifiers separated by "&#124;"), it is strongly recommended to have only one organism per protein per MITAB line. Currently no taxonomy identifiers other than NCBI taxid are anticipated, apart from the use of -2 to indicate "chemical synthesis" and -3 indicates "unknown". |
| checksum | 33 | 34 | represented as **methodName:value**, where methodName is the name of the corresponding checksum method, and value is the checksum for this interactor. Multiple checksums separated by "&#124;". This columns can contain for instance rogid, or standard inchi key |

<br />

It is recommended that the unique identifier and alternative identifier column should be used as follow:
  * unique identifier column: Ideally indicate a single reference to a chosen primary sequence database (e.g. one of UniProt or RefSeq). The unique identifier should not be ambiguous. If the interactor can match several RefSeq identifiers are used but only one master UniProt ac, it is recommended to give the master UniProt ac as 'unique identifier' and the RefSeq identifiers as 'alternative identifiers'.
  * alternative identifier column: any other database identifier referring to your interacting molecule. Here are two examples:
    * if you are UniProt centric, you could add mapping to RefSeq,
    * if you are a gene centric, you could add mapping to UniProt and/or RefSeq.

The first two columns 'unique identifier' should never be both empty columns. If a unique identifier to a sequence database cannot be found, it is important to give at least one identifier from the interaction database that created the interactor entry (Ex : IntAct accession, MINT accessions, etc.). One empty column is allowed in case of intra-molecular interactions (a single molecule interacts with itself). If one 'unique identifier' column is empty, it is expected to have empty columns for the matching 'alternative identifier', 'alias', 'taxid', 'interactor xref', 'checksum', 'biological role', 'experimental role', 'interactor type', 'feature', 'participant identification method'.

It is recommended to give gene names, ORF, locus names, gene synonyms, Chebi recommended name, drug name and/or protein recommended names in the alias columns.


Other cross references which can describe the interactors but ARE NOT identifiers such as GO xrefs could be added in columns 23 and 24.


In a single MITAB line, the interactors should only be associated with a single taxon id.


When it is available, a checksum of the interactor can be used in column 33 and 34 such as rogid, crogid and standard inchi key. These checksums could then be used for clustering interactors and taking into account their sequence.

Here is a recommendation for various molecule types:

#### 1. Complexes ####

In case of complexes (several protein chains for instance), no reference database can be recommended. The UniprotKB database does not generate unique identifiers for complexes. For now, only identifiers generated by the interaction databases can be used. For clustering purposes, if one interaction database such as IntAct did create an entry for describing a specific complex, the accession of the interaction generated by the database (IntAct) could be used across several different interaction databases to point to the same complex.

#### 2. Proteins ####

| **Column** | **Data required** | **Example(s)** |
|:-----------|:------------------|:---------------|
| Unique identifier | Use preferentially a single cross references to uniprotkb or RefSeq |`uniprotkb:P51587`<br /> `uniprotkb:P51123-3`<br /> `refseq:NP_000059`|
| Alternative identifier |  Use **secondary cross references** in primary database, <br /> Use model organism databases. | `uniprotkb:O00183` |
| Interactor Xrefs |  Use cross references to databases that can give more information about the protein but cannot be used as identifier. This columns can also contain secondary identifiers that are ambiguous (can be shared by two different proteins for instance, uniprot demerge) and that cannot be used to identify a single protein. | `go:"GO:0003824"` |
| Alias | use the gene name found in your reference database. 'orf name', 'gene name synonym', 'locus names' and 'protein recommended name' can also be added | `uniprotkb:BRCA2(gene name)` <br />`uniprotkb:FACD(gene name synonym)` |
| NCBI Taxonomy identifier | The taxid of the molecule (e.g. taxid:9606) should always be provided. In parenthesis, it is recommended to add the common name/scientific name of the organism. | `taxid:9606`<br /> `taxid:9606(human)`  <br /> `taxid:9606(Homo sapiens)` |
| Interactor checksums (columns 33 and 34) |  Use **rogid** and **crogid** | `rogid:UcdngwpTSS6hG/pvQGgpp40u67I9606` <br /> `crogid:UcdngwpTSS6hG/pvQGgpp40u67I9606` |

**What is a ROGID ?**

ROGID (Redundant Object Group Identifier) is a SHA-1 digest of the protein interactor's primary amino acid sequence concatenated with the NCBI taxonomy identifier. The first 27 character of a ROGID is always the hash value (SEGUID) to which is appended the taxid. Please refer to the [iRefIndex paper](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2573892) for more details.

**What is a CROGID ?**

This is similar to ROGID but allows the description of _Canonical_ Redundant Object Group. See below how a canonical sequence should be chosen.

#### 3. Small Molecules ####

| **Column** | **Data required** | **Example(s)** |
|:-----------|:------------------|:---------------|
| Unique identifier |  use the **standard inchi key** if not ambiguous, otherwise use a non ambiguous identifier (Chebi recommended). As the standard inchi key is not a database identifier but more a checksum, a unique Chebi identifier would be recommended. The standard inchi key should only be used as identifier for enrichment purposes and it may be moved to the checksum columns after data enrichment. If the standard inchi key is used as an identifier, the database is unknown and we should write standard inchi key in parenthesis | `unknown:"KTUFNOKKBVMGRW-UHFFFAOYSA-N"(standard inchi key)`|
| Alternative identifier | use cross references to **chebi** or other small molecule database that can identify without ambiguity the small molecule. | `chebi:"CHEBI:45783"`|
| Interactor Xrefs |  Use cross references to databases that can give more information about the small molecule but cannot be used as identifier. This columns can also contain secondary identifiers that are ambiguous (can be shared by two different small molecules for instance) and that cannot be used to identify a single molecule. | `pubchem:26697112` |
| Alias | add a **standard inchi**, **smile**, **Chebi name**, **drug name** | `unknown:"1S/C29H31N7O/c1-21-5-10-25(18-27(21)34-29-31-13-11-26(33-29)24-4-3-12-30-19-24)32-28(37)23-8-6-22(7-9-23)20-36-16-14-35(2)15-17-36/h3-13,18-19H,14-17,20H2,1-2H3,(H,32,37)(H,31,33,34)"(standard inchi)`<br />`chebi:imatinib(chebi name)`|
| NCBI Taxonomy identifier | it should be '-' if undefined, taxid:-3(unknown), taxid:-2(chemical synthesis) or a specific taxid if known|  |
| Interactor checksums (columns 33 and 34) |  Use **standard inchi key** | `standard inchi key:"KTUFNOKKBVMGRW-UHFFFAOYSA-N"` |

Should the Standard InCHI Key not describe unambiguously a molecule, the data provider should use an other cross reference and keep the Standard InCHI Key as a checksum only.

**What is a Standard InChI ?**

IUPAC International Chemical Identifier (InChI) - a machine-readable character string describing a chemical structure, developed by IUPAC and the InChI Trust as a standard to allow interoperability and linking between chemical resources.  The standard InChI differs from the non-standard InChI in that it is generated with a fixed set of parameters, ensuring consistency between different resources. The current version of the standard InChI software is 1.03.

**What is a Standard InChI Key ?**

The standard InChI Key is a condensed, 27 character identifier that is a hashed version of the full standard InChI (using the SHA-256 algorithm), designed to allow for easy web searches of chemical compounds.

The [InChI Trust](http://www.inchi-trust.org/?q=node/3) has more information and software support for InChI related matters.

#### 4. Nucleic Acids ####

| **Column** | **Data required** | **Example(s)** |
|------------|-------------------|----------------|
| Unique identifier | use a single cross references to **embl/genebank/ddbj**|`ddbj/embl/genbank:U41813` |
| Alternative identifier | use other cross references to other nucleotide sequence databases such as Refseq nucleotides  |  |
| NCBI Taxonomy identifier | The taxid of the molecule (e.g. taxid:9606) should be provided when available. In parenthesis, it is recommended to add the common name/scientific name of the organism. It should be '-' if undefined, taxid:-3(unknown) or taxid:-2(chemical synthesis) otherwise. ||


#### 5. Gene ####

This case is differentiated from 'Nucleic Acid' as not all nucleic acid sequence result in genes. Furthermore genes can be references to with set of public databases that differs from other Nucleic Acid based molecules.

| **Column** | **Data required** | **Example(s)** |
|:-----------|:------------------|:---------------|
| Unique identifier | use **a unique** cross references to **entrez gene/locuslink**, **ensembl**, or **ensemblGenome** | `entrez gene/locuslink:84665`<br />`ensembl:X63509`<br />`ensemblgenomes:AT1G66140`|
| Alternative identifier | use cross references to **entrez gene/locuslink**, **ensembl** and **ensemblGenome** that could not be used in 'unique identifier' columns. |  |
| Interactor Xrefs | use other cross references to other databases that can add more information about the gene but cannot be used as identifier |  |
| Alias | use gene names, ORF, locus names and/or gene synonyms |  |
| NCBI Taxonomy identifier | The taxid of the molecule (e.g. taxid:9606) should always be provided. In parenthesis, the common name and/or scientific name should be given | `taxid:9606(Homo sapiens)`<br />`taxid:9606(human)` |

### B. Describing the publication ###

Currently, the publication can be described using up to 2 columns in MITAB. The publication information should be provided because can be used for PSICQUIC queries, clustering, scoring and linking to the original publication.

| **Column** | **Data required** | **Example(s)** |
|:-----------|:------------------|:---------------|
| identifier of the publication (col 8) | use **a unique** cross references to pubmed or doi. If an IMEx id has been assigned to the publication, it should be added as well. If no pubmed id or DOI number can be used, another publication identifier could be used | `pubmed:10655498`<br />`pubmed:16980971`<br />`imex:IM-1`|
| First Author | use the first author surname in the publication and the publication date in parenthesis | `Ciferri et al.(2005)` |

### C. Describing the organism ###

In MITAB 2.7, three columns can describe organisms.

| **Column** | **Data required** | **Example(s)** |
|:-----------|:------------------|:---------------|
| NCBI Taxonomy identifier for interactor A (col 10 and 11) | use **a unique** taxId and in parenthesis gives the common name and/or scientific name. This information should always be provided for genes and proteins. For nucleic acids and small molecules, the column can be empty if the information is not relevant, -2 to indicate "chemical synthesis" and -3 to indicate "unknown"  | `taxid:9606(human)`<br />`taxid:9606(human)`<br />`taxid:9606(Homo sapiens)`|
| NCBI Taxonomy identifier for the host organism | use the taxId of the host organism only. -3 for unknown, -2 for chemical synthesis, -4 for in vivo and -5 for in sillico are allowed. In parenthesis, give the common name and/or scientific name of the organism. Cell types and tissues cannot be represented in this column. This information is recommended for MIMIx | `taxid:9606(human)`<br />`taxid:9606(human)`<br />`taxid:9606(Homo sapiens)` |

### D. Describing controlled vocabularies ###

In MITAB 2.7, 12 columns are controlled vocabulary columns :

  * MIMIx : interaction detection method (col 7), biological roles (col 17 and 18), experimental roles (col 19 and 20) and participant identification methods (col 41 and 42).
  * Complex expansion should always be provided in column 16 when the binary interaction has been expanded and was originally part of a n-ary interaction
  * IMEx : interaction type which can be used for scoring (col 12), interactor types which can be used to filter interactions (col 21 and 22)
  * source databases should always be provided in column 13

| **Column** | **Data format** | **Example(s)** |
|:-----------|:----------------|:---------------|
| columns 7, 12, 16, 17, 18, 19, 20, 21, 22, 41 and 42,   | use **a unique** cross references to the PSI-MI ontology. In parenthesis, it should be the name of the MI term in the ontology | `psi-mi:"MI:0914"(association)` |
| column 13 | use one to several cross references to the PSI-MI ontology depending on the interaction which can be imported from other databases. | `psi-mi:"MI:0469"(intact)`<br />`psi-mi:"MI:0923"(irefindex)` |

### E. Describing interaction and complex expansion ###

In MITAB 2.6 and MITAB 2.7, it is possible to tag n-ary interactions which have been expanded. When a binary intercation is expanded, the method to expand the complex should always be provided in column 16 for filtering and clustering purposes.

However, this information is not enough to be able to re-build a complex from MITAB. The interaction AC column could be used to retrieve all the binary pairs composing the complex if the interaction AC is unique per interaction (true binary and n-ary interactions). If possible, the column 14 (Interaction identifiers) should always give an identifier for this purpose (could be the database accession of the interaction or an automatically generated identifier). This only concerns data providers which expand n-ary interactions. In case of true binary interactions, the column 14 is only used for linking to the proper database entry.

_Ex :_
`psi-mi:"MI:1060"(spoke expansion)`
`psi-mi:"MI:1061"(matrix expansion)`
`psi-mi:"MI:1062"(bipartite expansion)`


Negative interactions can be represented in MITAB 2.6 and MITAB 2.6 but the negative column (column 36) should always be 'true'. The column can be left empty for positive interactions or should be 'false'.

Supplementary information could be given in column 25 (Interaction xrefs) such as GO xrefs.

### F. Describing annotations ###

In MITAB 2.6 and 2.7, it is possible to give annotations for interactors (col 26 and 27) and interaction which can be used for tagging (col 28). The topic of the interaction should always be provided (could be any participant attribute name in PSI-MI ontology for columns 26 and 27 and any interaction attribute name or curation content/curation quality tags in the PSI-MI ontology for column 28). The text is optional and if provided must be properly escaped (breakline, tabs, MITAB reserved characters).

The section K gives more information about how to tag interactions.

### G. Describing interaction parameters ###

| **Column** | **Data format** | **Example(s)** |
|:-----------|:----------------|:---------------|
| Paramaters of the interaction (col 30) | represented as type:value(text) where type is a parameter type name from the PSI-MI ontology. Multiple values can be separated by "&#124;". Special characters should not be allowed in MITAB so to represent exponents, fractions or the real values could be used. | kd:"2.34x1/100000" |

### H. Describing stoichiometry and self interactions ###

In MITAB 2.7, 2 columns can be used to specify the stoichiometry of the participants (columns 39 and 40). If no stoichiometry information are available, these columns should stay empty (-).
<br />

Three different cases need to be specified :

  * intra-molecular/auto-catalysis : only one interactor is given and the columns for the second interactor should all be empty (with a '-'). The stoichiometry of the interactor should be 1.
  * homodimers, trimers, etc. : two interactors are given (identifiers of interactor A are the same as identifiers for Interactor B). One of the stoichiometry column should be 0 and the other stoichiometry column should be a positive numeric value. _Ex: for homodimers, stoichiometry is 2_
  * homo oligomers : two interactors are given (identifiers of interactor A are the same as identifiers for Interactor B). Both stoichiometry columns should be 0.

### I. Describing features ###

Features of participant A and B can be added in columns 37 and 39 of MITAB 2.7.

| **Column** | **Data format** | **Example(s)** |
|:-----------|:----------------|:---------------|
| Features for interactor A and B | describe features or participant A such as binding sites, PTMs, tags, etc. Represented as feature\_type:range(text), where feature\_type is the feature type as described in the PSI-MI controlled vocabulary. For the PTMs, the MI ontology terms are obsolete and the PSI-MOD ontology should be used instead. The text can be used for feature type names, feature names, interpro cross references, etc. The use of the following characters is allowed to describe a range position : ‘?’ (undetermined position), ‘n’ (n terminal range), ‘c’ (c-terminal range), ‘>x’ (greater than x), ‘<’ (less than x), ‘x1..x1’ (fuzzy range position Ex : 5..5-9..10). The character '-' is used to separate start position(s) from end position(s). Multiple features separated by "&#124;". Multiple ranges per feature separated by ','. However, It is not possible to represent linked features/ranges | `sufficient to bind:27-195,201-133 (IPR000785)` <br /> `gst tag:n-n(n-terminal region)`<br />`sufficient to bind:23-45` <br /> `binding site:23..24-46,33-33` |

### J. Interaction confidence nomenclature ###

A scoring nomenclature has been discussed during the PSI meeting 2012 and no final decision has been reached yet.

The current proposal is :
<br />

_{service}-{score method}-{profile}_

  * service = Service or database which performed the score
  * score method = Name of the score method use to score interactions (CV term)
  * profile = Name used to define a specific way to calculate the score. This could include specific parameters or configuration for a scoring method.
"service", "score method" and "profile" would be optional, but at least one of them should be present.


_e.g._	
`intact-miscore-default:0.36  {service}-{score method}-{profile}`
`miscore-default:0.36         {score method}-{profile}`
`miscore-imex:0.20            {score method}-{profile}`
`miscore-psicquic:0.60        {score method}-{profile}`

This level of detail is important as the score will differ not only with method, but also with the dataset over which the score is run and the parameters set.

### K. Interaction Evidence Clustering ###

**What is clustering ?**

Storing in a single MITAB line the content of multiple interaction evidence. The format is (to an extent) capable of representing this data by concatenating information in the respective columns. Interaction clustering is an commonly requested operation on molecular interactions query results. This allows for instance to identify a non redundant set of interacting molecule pairs.

#### Should You Be Serving Clustered Data ? ####

Clustering can be performed by a data provider and the clustered data be served by PSICQUIC. However, this practice is not optimal as far as user queries are concerned. For instance. if a service is serving a clustered interaction that aggregates evidences detected by 'yeast two hybrid' and 'pull down' and the user searches for `NOT "yeast two hybrid"`, the clustered line containing pull down would not be returned. The same problem can be reported for a service that is clustering two interactors from two different organisms but with the same sequence in the same column.

#### Clustering Algorithms ####

Typically, clustering is performed by matching interacting molecule pairs using a predefined set of database cross references and aliases. For instance it could be performed by matching molecules based on !UniProtKB, RefSeq, rogid, chebi, standard inchi key. Hence, if the recommendation on how to describe an interacting molecule was followed, interaction evidence clustering should work efficiently.

#### How To Present Clustered Data in MITAB ####

Clustering is currently only run over the single line representation of data in the MITAB format, where multiples pieces of information are separated by ‘|’. As these pieces of information often do not have a 1:1 relationship, for example one interaction method may be related to multiple interaction types, relationships between information will inevitably be lost. There was some discussion and to whether it was worth retaining these relationships by duplicating information but it was generally agreed that the records would then be less human-readable (which is the main reason for producing MITAB in the first place), and that MITAB should only contain the summary of the cluster and in a long term solution, XML could be used for keeping the relationships.

<br />
### L. Interaction Evidence Tagging ###

Currently, PSICQUIC tagging is done by the PSICQUIC Registry. Tagging the PSICQUIC service in the registry is important because it gives information about the content of each PSICQUIC registry and can help to focus queries on specific services depending on what the user is looking for (mainly for optimisation). However, this tagging approach presents the obvious limitation that a service, which provides mixed datasets matching different tags, can only be in or out, as opposed to filtering the data it hosts. We will describe in this section some recommendation to implement tagging at the interaction evidence level.

**What tags are currently available ?**

The tags are fully integrated in the PSI-MI Ontology and they can be found [here](http://code.google.com/p/psicquic/wiki/PsicquicServiceTags).

**Tags useful at the interaction level**
<br />
  * mimix curation or rapid curation are useful. It is easy to detect interactions having imex-curation because they have an IMEx identifier in the interaction Acs column.
  * complex expansion tags will be used in a specific 'Complex expansion' column in MITAB 2.7
  * some data source tags are useful at the level of interaction such as 'imported', 'internally curated'. The tags 'predicted', 'experimentally-observed' and 'text-mining' could be deduced from the interaction detection method so can already been filtered without tagging. Depending on the data provider, it is not necessary to tag at the level of the interaction for the data-source because only contain one specific data source.
  * the interacting molecule tags such as protein-protein, nucleicacid-protein or smallmolecule-protein are not really necessary in MITAB 2.7 and MITAB 2.6 because of the Interactor type(s) columns. As an interactor type can be any children of protein. nucleic acid and small molecule, being able to tag the interaction could avoid going back to the ontology to recognize proteins from nucleic acids and small molecules. However, with the interactor type information, we could have more filtering options (peptide-protein, gene-gene, etc.) without the need of new controlled vocabulary terms.
  * the interaction representation tags (clustered or evidence) are not really important at the interaction level because all the data providers are now providing evidence based interactions and not clustered interactions.
  * the curation coverage (full-curation or partial-curation) are tags that are interesting to add at the interaction level.

**How to encode Tags ?**

In **MITAB2.7** onward it will be stored in column 28 (Interaction Annotation). The syntax for annotation columns in MITAB 2.7 is topic:text where topic is the annotation topic and text is free text. In the case of tags, only the topic will be given as described in the corresponding PSI-MI Ontology, example: `evidence` for the term 'evidence' (MI:1051).

In the **PSI-MI XML 2.5** format, these tags will be stored under the interaction's attribute, example: `<attribute name="evidence" nameAc="MI:1051" />`

<br />
### M. Molecule Naming for Network Visualisation ###

In the context of network visualisation, where molecules are typically nodes and interaction edges. Nodes are usually labelled with the name of the molecule is represents. It would be helpful if data providers could indicate a chosen name for their interacting molecule. This could be enabled easily by simply adding an additional alias formatted as follow: `psi-mi:label(display_short)`, where label is the chosen name for the molecule.

This topic has been discussed at the PSI-MI Spring meeting 2011 (Heidelberg) and 2012 (San Diego) and here is the consensus we have reached.

The group felt there was a need for two display names to be defined in order to reflect a **overview** (TODO: add MI CV for display short) and **detailed** (TODO: add MI CV for dislay long) naming of molecules. Examples of use will be given for specific molecule types below.

This information should be added by PSICQUIC data providers (and more generally MITAB producers) and stored under the respective aliases columns of molecule A and B (respectively 5 & 6). If not present, the Data Enricher could add this information. It has been agreed that it should be encoded as a `psi-mi` reference as this is the group that rubber stamped this specification.

> Examples:
    * `psi-mi:LSM7(display_short)`
    * `psi-mi:P12345-1_HUMAN(display_long)`

The recommendation is molecule type centric, the order column indicates the picking order depending on availability.

**Proteins**

| Order | Value | Level | Example(s) |
|:------|:------|:------|:-----------|
| 1 | Gene Symbol (gene name or gene synonym) | Overview | `psi-mi:LSM7(display_short)`|
| 2 | First sequence database identifier/accession | Detailed & Overview | `psi-mi:P53905(display_long)` |
| 3 | First available identifier | Detailed & Overview | `psi-mi:EBI-1234(display_long)` |

**Small Molecules**

| Order | Value | Level | Example(s) |
|:------|:------|:------|:-----------|
| 1 | ChEBI recommended name or drug name | Overview | `psi-mi:imatinib(display_short)` |
| 3 | First available identifier | Detailed & Overview | `psi-mi:CHEMBL340969(display_long)` |

**Nucleic Acids**

| Order | Value | Level | Example(s) |
|:------|:------|:------|:-----------|
| 1 | First available identifier | Overview and/or Detailed | `psi-mi:AF026397(display_long)` |

**Genes**

| Order | Value | Level | Example(s) |
|:------|:------|:------|:-----------|
| 1 | Gene symbol( gene name or synonyms ) ending with '_gene'_| Overview and/or Detailed | `psi-mi:LSM7_gene(display_short)` |
| 2 | First identifier | Overview and/or Detailed ||

It was agreed that in order to differentiate proteins (primarily described by gene symbol) from genes in a network display, we will append to the gene symbol the molecule type.