# MIQL 2.8 #

The Molecular Interactions Query Language (MIQL) defines a way to allow more powerful and flexible queries by using a specific syntax when doing searches. If we have a common way to access the data (PSICQUIC), we need a common way to write the search queries.
In most cases, searches are done for a specific identifier or group of identifiers. However, the service is not limited to these. For instance, there are ways to search for specific organisms, interaction detection methods or publication identifiers. The MIQL defines how these kind of queries can be done.

MIQL is a consensus between the different databases, so you should be able to use the same query across different repositories. It is based on the [PSIMITAB 2.8](MITAB28Format.md) format and allows to search for data in specific columns, by using the fields explained in the next section.

The MIQL syntax is based on [Lucene's syntax](http://lucene.apache.org/java/3_0_0/queryparsersyntax.html). A query is broken into terms and operators:

  * **Terms**: single words or phrases (group of words surrounded by quotes). E.g. <font color='#006600'><b><code>brca2</code></b></font> or <font color='#006600'><b><code>"pull down"</code></b></font>
  * **Fields**: used to search in a specific column. See the next section for the specific field names. E.g. <font color='#006600'> <b><code>species:human</code></b></font>
  * **Term modifiers**: wildcard searches, fuzzy searches, proximity and range searches. E.g. <font color='#006600'><b><code>brc*</code></b></font>
  * **Operands**: _OR_ (or space), _AND_, _NOT_, +, -. E.g. <font color='#006600'><b><code>brca2 AND rpa1</code></b></font>  or  <font color='#006600'><b><code>brca2 NOT mouse</code></b></font> or <font color='#006600'><b><code>+brca2 –mouse –complex:spoke</code></b></font>
  * **Grouping and field grouping**: <font color='#006600'><b><code>brca2 AND ( mouse "in vitro" )</code></b></font>

**IMPORTANT**: When using parenthesis in your queries, please add a space after and opening parenthesis and before a closing one, since some PSICQUIC implementations need it for correct parenthesis recognition.


# Fields #

The following table shows the available standard fields that can be used in PSICQUIC searches:

| **Field Name** | **Searches on** | **MITAB 2.8 Columns**| **Example** |
|:---------------|:----------------|:---------------------|:------------|
| idA | Identifier A | 1 | `idA:P74565` |
| idB | Identifier B | 2 |`idB:P74565` |
| id | Identifiers (A or B) | 1..4 | `id:P74565` |
| alias | Aliases (A or B) | 5, 6 | `alias:( KHDRBS1 OR HCK )` |
| identifier | Identifiers (A or B) or Alternatives (A or B)  Aliases (A or B) | 1..6 | `identifier:P74565` |
| pubauth | Publication 1st author(s) | 8 | `pubauth:scott` |
| pubid | Publication Identifier(s)  | 9 | `pubid:( 10837477 OR 12029088 )` |
| taxidA | Tax ID interactor A: be it the tax ID or the species name | 10 | `taxidA:mouse` |
| taxidB | Tax ID interactor B: be it the tax ID or species name | 11 | `taxidB:9606` |
| species | Species. Tax ID A and Tax ID B | 10, 11| `species:human` |
| type	| Interaction type(s) | 12 | `type:"physical association"` |
| detmethod | Interaction Detection method(s) | 7 | `detmethod:"two hybrid*"` |
| interaction\_id | Interaction identifier(s) | 14 | `interaction_id:EBI-761050` |
| pbioroleA | Biological role A | 17 | `pbioroleA:ancillary` |
| pbioroleB | Biological role B | 18 | `pbioroleB:"MI:0684"` |
| pbiorole | Biological roles (A or B) | 17, 18 | `pbiorole:enzyme` |
| ptypeA | Interactor type A | 21 | `ptypeA:protein` |
| ptypeB | Interactor type B | 22 | `ptypeB:"gene"` |
| ptype | Interactor types (A or B) | 21, 22 | `pbiorole:"small molecule"` |
| pxrefA | Interactor xref A (or Identifier A) | 23, 1 | `pxrefA:"GO:0003824"` |
| pxrefB | Interactor xref B (or Identifier B) | 24, 2 | `pxrefB:"GO:0003824"` |
| pxref | Interactor xrefs (A or B or Identifier A or Identifier B) | 23, 24, 1, 2 | `pxref:"catalytic activity"` |
| xref | Interaction xrefs (or Interaction identifiers) | 25, 14 | `xref:nuclear pore` |
| annot | Interaction annotations and tags | 28 | `annot:"internally curated"` |
| udate | Update date | 32 | `udate:[20100101 TO 20120101]` |
| negative | Negative interaction boolean | 36 | `negative:true` |
| complex | Complex expansion | 16 | `complex:"spoke expanded"` or `complex:"MI:1060"` |
| ftypeA | Feature type of participant A | 37 | `ftypeA:"sufficient to bind"` |
| ftypeB | Feature type of participant B | 38 | `ftypeB:mutation` |
| ftype | Feature type of participant A or B | 37, 38 | `ftype:"binding site"` |
| pmethodA | Participant identification method A | 41 | `pmethodA:"western blot"` |
| pmethodB | Participant identification method B | 42 | `pmethodB:"sequence tag identification"` |
| pmethod | Participant identification methods (A or B) | 41, 42 | `pmethod:immunostaining` |
| stc | Stoichiometry (A or B). Only true or false, just to be able to filter interaction having stoichiometry available | 39, 40 | `stc:true` |
| param | Interaction parameters. Only true or false, just to be able to filter interaction having parameters available | 30 | `param:true` |
| bioeffectA | Biological effect of participant A | 43 | `bioeffectA:"kinase activity"` |
| bioeffectB | Biological effect of participant B | 44 | `bioeffectB:"antioxidant activity"` |
| bioeffect | Biological effect of participant A or B | 43, 44 | `bioeffect:"molecular carrier activity"` |
| causalmechanism | The indirect causal regulatory mechanism between participants A and B  | 45 | `causalmechanism:"MI:2245"` |
| causalstatement | The causal statement describing the effect of participant A on participant B | 46 | `causalstatement:"up regulates"` |