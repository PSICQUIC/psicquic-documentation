# Introduction #

The Molecular Interactions Query Language (MIQL) defines a way to allow more powerful and flexible queries by using a specific syntax when doing searches. If we have a common way to access the data (PSICQUIC), we need a common way to write the search queries.
In most cases, searches are done for a specific identifier or group of identifiers. However, the service is not limited to these. For instance, there are ways to search for specific organisms, interaction detection methods or publication identifiers. The MIQL defines how these kind of queries can be done.

MIQL is a consensus between the different databases, so you should be able to use the same query across different repositories. It is based on the PSIMITAB format and allows to search for data in specific columns, by using the fields explained in the next section.

The MIQL syntax is based on [Lucene's syntax](http://lucene.apache.org/java/3_0_0/queryparsersyntax.html). A query is broken into terms and operators:

  * **Terms**: single words or phrases (group of words surrounded by quotes). E.g. <font color='#006600'><b><code>brca2</code></b></font> or <font color='#006600'><b><code>"pull down"</code></b></font>
  * **Fields**: used to search in a specific column. See the next section for the specific field names. E.g. <font color='#006600'> <b><code>species:human</code></b></font>
  * **Term modifiers**: wildcard searches, fuzzy searches, proximity and range searches. E.g. <font color='#006600'><b><code>brc*</code></b></font>
  * **Operands**: _OR_ (or space), _AND_, _NOT_, +, -. E.g. <font color='#006600'><b><code>brca2 AND rpa1</code></b></font>  or  <font color='#006600'><b><code>brca2 NOT mouse</code></b></font> or <font color='#006600'><b><code>+brca2 –mouse –expansion:spoke</code></b></font>
  * **Grouping and field grouping**: <font color='#006600'><b><code>brca2 AND (mouse "in vitro")</code></b></font>

# Existing versions #

There are two versions of MIQL language which have been implemented so far.
  * [MIQL 2.5](http://code.google.com/p/psicquic/wiki/MiqlReference) is based on the [PSIMITAB 2.5](http://code.google.com/p/psicquic/wiki/MITAB25Format) format
  * [MIQL 2.7](http://code.google.com/p/psicquic/wiki/MiqlReference27) is an extension of MIQL 2.5 and is based on the [PSIMITAB 2.7](https://github.com/MICommunity/psicquic/blob/wiki/MITAB27Format.md) format.
