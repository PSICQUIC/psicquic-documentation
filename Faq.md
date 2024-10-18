

<br />

## Are there guidelines on how to create valid PSIMITAB ? ##
The original format (version 2.5) itself was first described in [Kerrien et al. (2007)](http://www.ncbi.nlm.nih.gov/pubmed/17925023) but you can also find it as part of the PSI-MI and PSICQUIC documentation. These documents only describe the various columns of the PSIMITAB format (2.5, 2.6, 2.7 and 2.8) and the syntax of the data that can be stored. In addition to the format, the PSI-MI workgroup has defined a guideline referred to as [Data Distribution Best Practices](DataDistributionBestPractices.md) that aims at standardising the use of the format to maximize its effectiveness. It is strongly recommended to read these documents before attempting to build a dataset using the [PSIMITAB 2.5](MITAB25Format.md), [PSIMITAB 2.6](MITAB26Format.md), [PSIMITAB 2.7](MITAB27Format.md) or [PSIMITAB 2.8](MITAB28Format.md) format.
<br />


## What identifier should I use to describe my Interacting Proteins ? ##
Most PSICQUIC providers are using UniProtKB ACs to describe their proteins, and this allows these services to be easily combined together. For more information, look at the [Data Distribution Best Practices](DataDistributionBestPractices.md).
<br />



## How can I map my identifiers to UniProtKB AC ? ##
If you happen to be using another identifier space to describe your proteins, there are several tools you could be using to map to UniProtKB:
  * [PICR](http://www.ebi.ac.uk/Tools/picr/)
  * [UniProt Mapping](http://www.uniprot.org/?tab=mapping)
<br />

## Why are my ChEBI identifiers not linked properly in PSICQUIC View ##
If you are using ChEBI, or any database identifier using reserved character such as column (':') you will have to escape them as follow: `CHEBI:"CHEBI:114264"`.


## How can I easily browse the various ontology types of PSI-MI ? ##
We recommend you use the [Ontology Lookup Service (OLS)](http://www.ebi.ac.uk/ontology-lookup/). You can browse the PSI-MI ontology as a simple tree structure here or perform the following searches from the OLS home page:
search by term name (with auto-completion),
search by term id.
<br />



## Can I cluster multiple interaction evidences into a single MITAB line ? ##
Yes you can, but we do not recommend you doing it if you are intending to distribute the data using PSICQUIC. While PSICQUIC isn’t affected by clustered data, it doesn’t allow users to effectively query the service.

Let’s describe the issue using an example, say you have 2 MITAB lines:
```
 P12345	Q98765	-	-	-	-	two hybrid	…
 P12345	Q98765	-	-	-	-	coip	…
```

Now let’s consider the clustered equivalent of these 2 lines:
```
 P12345	Q98765	-	-	-	-	two hybrid|coip	…
```

So now if a user queries the non-clustered service with the following MIQL:
```
NOT detmethod:coip
```

the response contains a single line (i.e. the two hybrid evidence).
When the user runs the same query on the clustered service, the response shows no data because the whole line has been removed as it contains a coip evidence, leading the user to miss potentially critical information.
<br />



## How do I define confidence values ? ##
Column 15 of MITAB was designed to accommodate this type of data. There are numerous methods in used and in most cases, data providers tend to design their own. For this reason, we have defined a set of controlled vocabulary terms to help categorising broad classes of scoring methods. You can view the current list on the [Ontology Lookup Service](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MI&termId=MI%3A1064&termName=interaction%20confidence).
<br />


## How much additional information (i.e. alternative identifiers, aliases) should I add about my interacting molecules ? ##
While providing a UniProtKB AC is a great start to providing a broadly accepted referencing system for your proteins, many users are searching PSICQUIC services using gene names. For this reason, columns 5 and 6 will allow the storage of aliases for, respectively, molecule A and B. It is strongly encouraged to stored in these columns information such as:
  * `gene name (e.g. uniprotkb:BRCA2(gene name))`
  * `orf name (e.g.uniprotkb:F14J9.23(orf name))`
  * `locus name (e.g. uniprotkb:At1g09570(locus name))`
  * `gene name synonym (e.g. uniprotkb:Protein ELONGATED HYPOCOTYL 8(gene name synonym))`
The data type that can be used are defined in this branch of the [PSI-MI ontology](http://www.ebi.ac.uk/ontology-lookup/browse.do?ontName=MI&termId=MI%3A0300&termName=alias%20type).
<br />



## How should I use the Unique Identifier/Alternative Identifier columns ? ##
These columns have different purposes, all of which are geared toward identifying the interacting molecule unambiguously. While the unique identifier is meant as a single cross reference to a public database, the alternative identifier column should be used to maintain a collection of alternative identifiers potentially encompassing secondary identifiers (e.g. UniProtKB), model organism databases (SGD, FlyBase...), translation to other biological concept (e.g. the molecule descibed is a protein but I could store an ensembl or entrez geneid). The [Data Distribution Best Practices](DataDistributionBestPractices.md) does give some additional information with respect to which specific cross reference to use.
