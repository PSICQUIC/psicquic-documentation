# MIQL 2.5 #

The Molecular Interactions Query Language (MIQL) defines a way to allow more powerful and flexible queries by using a specific syntax when doing searches. If we have a common way to access the data (PSICQUIC), we need a common way to write the search queries.
In most cases, searches are done for a specific identifier or group of identifiers. However, the service is not limited to these. For instance, there are ways to search for specific organisms, interaction detection methods or publication identifiers. The MIQL defines how these kind of queries can be done.

MIQL is a consensus between the different databases, so you should be able to use the same query across different repositories. It is based on the [PSIMITAB 2.5](http://code.google.com/p/psicquic/wiki/MITAB25Format) format and allows to search for data in specific columns, by using the fields explained in the next section.

The MIQL syntax is based on [Lucene's syntax](http://lucene.apache.org/java/3_0_0/queryparsersyntax.html). A query is broken into terms and operators:

  * **Terms**: single words or phrases (group of words surrounded by quotes). E.g. <font color='#006600'><b><code>brca2</code></b></font> or <font color='#006600'><b><code>"pull down"</code></b></font>
  * **Fields**: used to search in a specific column. See the next section for the specific field names. E.g. <font color='#006600'> <b><code>species:human</code></b></font>
  * **Term modifiers**: wildcard searches, fuzzy searches, proximity and range searches. E.g. <font color='#006600'><b><code>brc*</code></b></font>
  * **Operands**: _OR_ (or space), _AND_, _NOT_, +, -. E.g. <font color='#006600'><b><code>brca2 AND rpa1</code></b></font>  or  <font color='#006600'><b><code>brca2 NOT mouse</code></b></font> or <font color='#006600'><b><code>+brca2 –mouse </code></b></font>
  * **Grouping and field grouping**: <font color='#006600'><b><code>brca2 AND (mouse "in vitro")</code></b></font>


# Fields #

The following table shows the available standard fields that can be used in PSICQUIC searches:

| **Field Name** | **Searches on** | **MITAB 2.5 Columns**| **Example** |
|:---------------|:----------------|:---------------------|:------------|
| idA | Identifier A | 1 | `idA:P74565` |
| idB | Identifier B | 2 |`idB:P74565` |
| id | Identifiers (A or B) | 1..4 | `id:P74565` |
| alias | Aliases (A or B) | 5, 6 | `alias:(KHDRBS1 OR HCK)` |
| identifier | Identifiers (A or B) or Aliases (A or B) | 1..6 | `identifier:P74565` |
| pubauth | Publication 1st author(s) | 8 | `pubauth:scott` |
| pubid | Publication Identifier(s)  | 9 | `pubid:(10837477 OR 12029088)` |
| taxidA | Tax ID interactor A: be it the tax ID or the species name | 10 | `taxidA:mouse` |
| taxidB | Tax ID interactor B: be it the tax ID or species name | 11 | `taxidB:9606` |
| species | Species. Tax ID A and Tax ID B | 10, 11| `species:human` |
| type	| Interaction type(s) | 12 | `type:"physical association"` |
| detmethod | Interaction Detection method(s) | 7 | `detmethod:"two hybrid*"` |
| source | Interaction source(s) | 13 | `psi-mi:"MI:0469"(intact) |
| interaction\_id | Interaction identifier(s) | 14 | `interaction_id:EBI-761050` |