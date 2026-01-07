# PSI-MI Feature TAB Format #

## Introduction ##

PSI-MI FeatureTab is a new format, it takes inspiration from the existing PSI-MI TAB 2,8 (1), which is actively supported by the MI worktrack. Most users will continue to use PSI-MI MITAB or PSI-MI XML2.5/3.0 to exchange experimental-based interaction data, the PSI-MI FeatureTab will be required only for specialist use cases, as for example, parsing all the molecular interaction data where mutations have been shown to affect a protein interaction.

(1) https://europepmc.org/article/MED/30793173


## Column definitions ##

The column contents should be as follows:

1. **Feature AC**, is designed to report the accession number for a feature such as mutations, binding sites, PTMs, etc. (ex. EBI-489661; EBI-1000504; EBI-1234567).
1. **Feature short label**, contains human-readable short label summarizing the amino acid changes and their positions.  In the case of sequence mutation features these are compliant with the Human Genome Variation Society recommendations (see https://hgvs-nomenclature.org/stable/recommendations/general/).
1. **Feature range(s)**, contains position(s) in the molecule sequence involved in that specific feature (Ex: mutation (ex. 255-255), binding sites (ex. 12-153), PTMs (ex. 15-15), etc).
1. **Original sequence**, contains the wild type molecule residue(s) affected, in one letter amino acid or nucleotide code.
1. **Resulting sequence**, contains the replacement sequence (or deletion) in one letter amino acid or nucleotide code.
1. **Feature type**, contains the feature type, following the PSI-MI controlled vocabularies (EX: mutation (MI:0118); mutation decreasing (MI:0119); mutation disrupting strength (MI:1128); Necessary binding region (MI:0429), etc.)
1. **Feature annotation**, contains specific comments, in free text, about the annotated feature that can be of interest.
1. **Affected molecule identifier**, contains affected molecule identifier (for proteins, preferably UniProtKB accession, if available, Ex: UniProtKB:P12346. ChEBI identifiers are recommended for small molecules and RNACentral identifiers for noncoding RNAs). It is represented as databaseName:identifier, where databaseName is the name of the corresponding database as defined in the [PSI-MI controlled vocabulary](https://www.ebi.ac.uk/ols4/ontologies/mi/classes/http%253A%252F%252Fpurl.obolibrary.org%252Fobo%252FMI_0444), and identifier is the unique primary identifier of the molecule in the database.
1. **Affected molecule symbol**, contains, for example, the gene name of the protein affected by a specific feature, as given by UniProtKB (EX. Gene name, DLG4).
1. **Affected molecule full name**, contains, for example, the full name of the protein affected by a specific feature, as given by UniProtKB (EX. DLG4, Disks large homolog 4).
1. **Affected molecule organism**, contains the TaxID and species name when the molecule is genome encoded as given by the NCBI taxonomy database. It is represented as taxid:identifier(organism name) where the identifier is the taxon id of the organism and organism name can either be the common name or scientific name (EX. 9606 – Homo sapiens).The use of the term  ‘Chemical synthesis’ is acceptable for small molecules.
1. **Interaction participants**, contains information about the identifiers for all participants in the affected interaction, along with their species and molecule type between brackets. Ex.: (UniprotKB:P15153(protein(MI:0326), 9606 – Homo sapiens)|ensembl:ENSP00000356505(protein(MI:0326), 9606 – Homo sapiens)).
1. **PubMed ID**, contains the reference to the publication where the interaction evidence was reported. It is recommended to give one PubMed ID per MITAB line and IMEx IDs can be added. Ex: PubMed:16980971|IMEx:IM-1
1. **Figure legend**, contains the reference to the specific figures or tables in the paper where the interaction evidence was reported.
1. **Interaction AC**, describes the interaction accession within our databases. This can be used to obtain further information about the interaction (EX.: EBI-489644; EBI-8285478).
1. **Xref ID**, contains whenever is available the Xref Identifier associated to a feature. It is represented as databaseName:ac(text), where databaseName is the name of the corresponding database as defined in the [PSI-MI controlled vocabulary](https://www.ebi.ac.uk/ols4/ontologies/mi/classes/http%253A%252F%252Fpurl.obolibrary.org%252Fobo%252FMI_0444), and ac is the primary accession in the database. For example, the InterPro cross references associated to a protein binding domain ((EX. Feature AC=EBI-7665833; INTERPRO_ID=IPR001478)). Multiple cross references are separated by “|”.

Empty columns should be represented with '-' to keep track of the columns.

## Syntax ##

Columns are normally formed by fields delimited by "|", with a structure like this one:

```
<XREF>:<VALUE>(<DESCRIPTION>)
```

Due to the unsafe use of reserved characters in the values, we have recently added the possibility to surround `<XREF>`, `<VALUE>` or `<DESCRIPTION>` with quotes if they contain a special symbol.

In MI-TAB, the reserved characters are:

```
|
(
)
:
\t (tabulation)
```

Whenever this happen in your data, surround the value with double quotes:

```
"<XREF_WITH_RESERVED_CHARS>":"<VALUE_WITH_RESERVED_CHARS>"("<DESCRIPTION>")
```

Note that the quotes are before and after each part. The escaped data should look like in the following examples:

```
psi-mi:"MI:0000"(a cv term)
psi-mi:"MI:0000"("I can now use braces ()()() or pipes ||| here and ::colons::")
```
If you want to use a quote within a quote, escape it:

```
uniprotkb:P12345("a \"nice\" protein")
```
