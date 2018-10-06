

## Purpose ##

One of the aim of this guideline is to provide the community with a tool that could help adding useful information to an existing MITAB 2.7 dataset (but because MITAB 2.7 is backward compatible with MITAB 2.5 and 2.6, the enricher can be used in MITAB 2.5 and 2.6 but will add less information than in MITAB 2.7). A tool, (referred later on as “Enricher”) could consume MITAB data, add extra information about molecules, controlled vocabularies, publication and return enriched MITAB content which follows the [Data best practices](DataDistributionBestPractices.md). Below are a few data items that could be enriched automatically:
  * molecule identifiers, aliases, xrefs and checksum
  * Controlled vocabulary terms could have their names added provided an ontology identifier is present, eg:
    * interaction detection method (column #7),
    * interaction type (column #12),
    * source database (column #13);
    * complex expansion (column #16);
    * biological roles (columns #17 and #18),
    * experimental roles (columns #19 and #20),
    * interactor types (columns #21 and #22),
    * participant identification methods (columns #41 and #42)
  * publication information such as author name (column #8) could be added provided there is a publication identifier (i.e. PMID);
  * organism name (columns #10 & 11) could be added if a taxid is provided.

## Data Enricher ##

The Enricher could use the following resources to retrieve data:
  * [Ontology Lookup Service](http://www.ebi.ac.uk/ontology-lookup/) (aka. OLS) to access the psi-mi ontology;
  * [CiteExplore](http://www.ebi.ac.uk/citexplore/) to access publication details;
  * [UniProtKB](http://www.uniprot.org/) to access protein information, the sequence information could then be used to compute ROGID and CROGID;
  * [UniProt Taxonomy](http://www.uniprot.org/taxonomy/) to access species information;
  * [PICR](http://www.ebi.ac.uk/Tools/picr/) to perform computational mapping of protein identifier;
  * [ChEBI](http://www.ebi.ac.uk/chebi/) to access small molecule information,

### Molecule enrichment ###

The Data enricher would use the identifiers in columns 1 and 2 (unique identifier) to collect information in PICR, UniProtKB and ChEBI. Here is a recommendation for various molecule types:

#### 1. Proteins ####

For higher organisms, the curator may have several isoforms of a protein to select from. In most cases, the experimental evidence will not be sufficient to make an unambiguous mapping. In such a case, most protein interaction databases will make a mapping to the canonical UniProtKB sequence e.g. P51123 to indicate that the interaction could be with some or all of the potential isoforms. Where a mapping to a specific isoform e.g. P51123-3 can be made, it will be. Gene-centric databases will map to the gene identifier in all cases. Whenever the curator has chosen a specific splice variant, its identifier should appear under the unique identifier column. Some examples of annotated proteins:

|    |    |
|:---|:---|
|ensembl:ENSG00000136869|innatedb:IDBG-82738|
|uniprotkb:O00206|uniprotkb:TLR4\_HUMAN|
|refseq:NM\_138554|refseq:NP\_612564|
|refseq:NR\_024169|refseq:NR\_024168|

**How to pick the canonical sequence for a given protein ?**

The sequence defined at the top level of a UniProtKB entry is considered a canonical sequence i.e. P51123. All isoforms linked to this entries (having their own potential sequence variation) would link to this top level sequence which is the canonical sequence for the entry (note, it will be an exact match to one of the isoforms). For example: should your molecule be P51123-3, the canonical sequence would be P51123.
Should the protein be described using a gene identifier (as seen in a minority of PSICQUIC services), it is recommended to map this identifier to the corresponding UniProt/Swiss-Prot canonical sequence, given a specific species, there should be only one corresponding UniProt/Swiss-Prot entry. If the entry is only in UniProtKB/TrEMBL, selecting the longest ORF for that gene is the conventional method for performing a 1:1 mapping.

**How to map UniProtKB proteins to RefSeq ?**

Some proteins may have related isoforms resulting from different splice isoforms of the mRNA or from alternative promoter usage. UniProtKB does give different identifiers to these entities and it is possible to map them to RefSeq by using the [PICR Identifier mapping](http://www.ebi.ac.uk/Tools/picr) service. In case of isoforms, PICR would be able to map it to the corresponding RefSeq identifier.

**How would it work in practice ?**

For proteins, the Data Enricher can:
  * remap identifiers from any databases listed in [PICR](http://www.ebi.ac.uk/Tools/picr/) to a single UniProtKB identifier when possible. For that, it is important to give unambiguous identifiers in columns 1 and 2 and to give the organism of the protein in columns 10 and 11. The organism is very important to be able to remap to a single uniprot accession. The Data Enricher will always remap to the master uniprot entry (canonical sequence) even if an identifier can match a single uniprot splice variant identifier. When the remapping is successful, the Enricher will not delete the original identifier but just move it to 'alternative identifiers' in columns 3 and 4 and add the remapped uniprot accession in columns 1 and 2 for 'unique identifier'. In several cases, the remapping is too ambiguous and the enricher would not enrich the line but just log a warning:
    * Several Swissprot entries can match
    * Several Trembl entries can match and have the same sequence length (but different sequences)
    * Identifier cannot be remapped to a UniProtKb accession
  * add Refseq identifiers using PICR. The Data Enricher will add all the possible Refseq identifiers in the columns 3 and 4 'Alternatice identifiers'.
  * enrich several columns :
    * In columns 5 and 6 for aliases, it will add gene name, gene synonym, protein recommended name, ORF and locus name. It will follow the Data best practices and add display\_short and display\_long aliases.
    * In columns 3 and 4 for alternative identifiers, it will add uniprotKb secondary accession when not ambiguous
    * In columns 23 and 24 for Interactor xrefs, it could add GO and interpro xrefs...
    * In columns 33 and 34 for Interactor checksums, it would add rogid and crogid

| **Protein accession** | **ROGID** | **CROGID** | **RefSeq** |
|:----------------------|:----------|:-----------|:-----------|
| `P51123`   | `rogid:DxUDrj8iljY131pQOBswejQxoxI7227` | `rogid:DxUDrj8iljY131pQOBswejQxoxI7227` | `NP_996160` |
| `P51123-2` | `rogid:nqWqHc3mUUZtYVGzCr3UZq60DRU7227` | `rogid:DxUDrj8iljY131pQOBswejQxoxI7227` | `NP_476956` |

<br />

| What information | Target Column | Data source |
|:-----------------|:--------------|:------------|
| gene name, gene name synonym, orf, locus name, recommended name, display\_short and display\_long | 5 & 6 | UniProtKB |
| Additional database cross references (e.g. primary database identifier such as RefSeq or UniProt), uniprot secondary AC | 3 & 4 | UniProtKB, PICR |
| Organism name (only if no conflicts with uniprot entry) | 10 & 11 | UniProt Taxonomy |
| Model organism database (Flybase, TAIR, SGD...), GO, interpro,... | 23 & 24 | UniProtKB |
| ROGID, CROGID | 33 & 34 | UniProtKB |


#### 2. Small Molecules ####

Should the Standard InCHI Key not describe unambiguously a molecule, the data provider should use an other cross reference and keep the Standard InCHI Key as an alternative identifier.

##### Enrichment Process #####

For small molecules, the Data Enricher can :
  * remap identifiers from any databases cross referenced by ChEBI (some Drugbank identifiers, Pubchem, etc.) to a single ChEBI identifier when possible. For that, it is important to give unambiguous identifiers or standard Inchi keys in columns 1 and 2 and to give the organism of the small molecule in columns 10 and 11 when relevant. The organism could help to remap to a single ChEBI identifier. When giving the standard inchi key in column 1 and 2 or 3 and 4, it should be represented as 'unknown:xxxxx(standard inchi key)'. The Data Enricher will remap to manually curated compounds when it is possible. When the remapping is successful, the Enricher will not delete the original identifier but just move it to 'alternative identifiers' in columns 3 and 4 and add the remapped ChEBI accession in columns 1 and 2 for 'unique identifier'. If the original identifier is a standard inchi key, it will move it to the checksum columns 33 and 34. In several cases, the remapping is too ambiguous and the enricher would not enrich the line but just log a warning:
    * Several compounds can match
    * Identifier cannot be found in ChEBI
  * enrich several columns :
    * In columns 5 and 6 for aliases, it will add ChEBI name, standard inchi. It will follow the Data best practices and add display\_short and display\_long aliases.
    * In columns 3 and 4 for alternative identifiers, it will add ChEBI secondary accessions when not ambiguous
    * In columns 23 and 24 for Interactor xrefs, it could add PubChem or other xrefs (To be defined)...
    * In columns 33 and 34 for Interactor checksums, it would add standard inchi key and maybe smiles as well.
The enrichment process here would rely on the existence of a !ChEBI identifier in the unique identifier column. If the given identifier is unambiguously identifying a single small molecule and the taxids match, the enrichment below can take place.

| What information | Target Column | Data source |
|:-----------------|:--------------|:------------|
| standard inchi, ChEBI name, display\_sort and display\_long | 5 & 6 | ChEBI |
| ChEBI secondary acs and Standard InChI | 3 & 4 | ChEBI |
| Organism name (only if no conflicts with ChEBI entry) | 10 & 11 | ChEBI and uniprot taxonomy |
| other xrefs which could be useful (to be defined) | 23 & 24 | ChEBI |
| standard inchi key, smile | 33 & 34 | ChEBI |


#### 3. Nucleic Acids and genes ####

It was agreed during the PSI meeting 2012 that the Data Enricher will not enrich genes and nucleic acids. It will be up to the data provider to follow the data best practices and provide:

  * unique embl/ddbj/genbank identifier for small nucleic acids in columns 1 and 2. It is recommended to move the other identifiers to alternative identifiers and Interactor xrefs.
  * unique ensembl genome, ensembl or gene id/locus link identifier for genes in columns 1 and 2. It is recommended to move the other identifiers to alternative identifiers and Interactor xrefs.
  * gene names should be provided for genes in aliases columns as well as display\_short and display\_long.
  * organisms will be enriched using uniprot taxonomy but it will not check if there is a conflict with the identifiers

### Organism enrichment ###

To be able to enrich the organism, it is important to give the taxid of the organism represented as 'taxid:taxon(text)'.

In case of proteins and small molecules, the organism enrichment will depend on the consistency between organism and the molecule identifiers.

##### Enrichment Process #####

For organisms (interactor organisms in columns 10 and 11 and host organism in column 29), the Data Enricher can:

  * add the missing organism for proteins and small molecules (and genes as well?) when possible (columns 10 and 11 only)
  * add the common name and scientific name as defined in the data best practices (columns 10, 11 and 29)

### Publication enrichment ###

To be able to enrich the publication, a pubmed id (or IMEx id) is necessary in column 9 (identifier of the publication).

##### Enrichment Process #####

For publications, the Data Enricher can:

  * For each pubmed id, it will add the first author name and publication date as defined in the data best practices

### Controlled vocabulary enrichment ###

The Data Enricher will only enrich psi-mi ontology terms in columns 7, 13, 12, 16, 17, 18, 19, 20, 21, 22, 41 and 42 (cross references to psi-mi terms should be represented with 'psi-mi:"MI:xxxx"(term name)').

The Enricher will only add the term name in parenthesis if it is missing or not exact.

For other ontology terms such as GO that could be present in columns 23,24 and 25 (interactor and interaction xrefs), the enricher could also add the name in parenthesis.