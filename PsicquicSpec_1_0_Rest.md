# Version 1.0 #

PSICQUIC is meant to be a RESTful service. Hence, it is possible to retrieve data using simple URLs through HTTP.

[SOAP](PsicquicSpec_1_0_Soap.md) can be too cumbersome for some users or developers as usually a client may be needed. With REST, none of this is necessary because it is possible to do a query through HTTP and get the data back. The simplest way to do it is to do queries using your browser, but REST is a convenient way to access the data for scripts.

Different methods are available using REST. It is possible to fetch data by using:

  * One or many interactor/participant identifiers.
  * One or many interaction identifiers.
  * A [MIQL](MiqlDefinition.md) flexible query.

The first two methods are just a convenient modification of the third method. The only difference is that the appropriate MIQL field is automatically added for you behind the scenes.

## URL syntax ##

The structure of the URL to fetch data from PSICQUIC is this one:

<img width='800' src='http://psicquic.googlecode.com/svn/wiki/images/rest_url/PSICQUIC_REST_URL.png' />

e.g. http://www.ebi.ac.uk/Tools/webservices/psicquic/intact/webservices/current/search/query/species:human?firstResult=0&maxResults=100

The URL contains different parts:

#### PSICQUIC\_URL ####

The first element of the URL is, of course, the location of the web service. Check the page for the [providers](PsicquicServiceProviders.md) for specific addresses.

#### VERSION ####

At this moment four versions of PSICQUIC exist. With time, more versions might exist. The possible values for this bit are:

| **Version** | **Description** |
|:------------|:----------------|
| v1.0 | Version 1.0 of the PSICQUIC specification |
| v1.1 | Version 1.1 of the PSICQUIC specification |
| v1.2 | Version 1.2 of the PSICQUIC specification |
| v1.3 | Version 1.3 of the PSICQUIC specification |
| current | Will map always to the most current version. It works as a symbolic link |

#### METHODS TO RETRIEVE MOLECULAR INTERACTION DATA ####

As we said before, there are different methods available to retrieve data:

| **Method** | **Since spec version** **Description** |
|:-----------|:---------------------------------------|
| interactor | v1.0 | To search using interactor identifiers or aliases |
| interaction | v1.0 | To search using interaction identifiers |
| query | v1.0 | To search using [MIQL](MiqlDefinition.md) queries |


#### METHODS WITH INFORMATION ABOUT THE SERVICE ####

These metadata methods return information about the service:

| formats | v1.0 | Lists the return formats supported by the service |
|:--------|:-----|:--------------------------------------------------|
| version | v1.0 | Implementation version |

#### QUERY ####

This is the place where we define the actual query. Depending on the method different queries may be used. When searching for interactors or interactions, the query must be one or many identifiers separater by the operands AND or OR (e.g. `facd AND brca2`).
When using the query method, the query can be anything.

For users accessing RESTful PSICQUIC using scripts, the query must be [properly encoded](http://en.wikipedia.org/wiki/Percent-encoding) to avoid illegal URIs. For instance, all spaces in the query must be replaced by _%20_. Most programming languages contain already methods to do this. For clever web browsers, this is not necessary.

#### PARAMETERS ####

Whereas the rest of parts of the URL are mandatory, parameters are optional. We can use the parameters to choose the output format or to paginate the query. The parameters available in the reference implementation are the following:

| **Parameter Name** | **Possible values** |
|:-------------------|:--------------------|
| format           | **xml25** (PSI-MIXML 2.5)<br> <b>tab25</b> (PSI-MITAB 2.5) <br> <b>tab26</b> (PSI-MITAB 2.6, not all data providers provide this format) <br> <b>tab27</b> (PSI-MITAB 2.7, not all data providers provide this format)<br><b>count</b> (Just the total count) <br>
<tr><td> firstResult </td><td> Integer value that defines the first element to be shown. If the whole result set contains 100 interactions and we use firstResult=40, the first row to be returned will be the 40 </td></tr>
<tr><td> maxResults </td><td> Integer value that defines the maximum number of interactions to be returned. For instance, a value of maxResults=20 will limit the results to 20 interactions. </td></tr></tbody></table>

It is possible to iterate through the results using "pages" by changing the value of <i>firstResult</i> while maintaining an immutable <i>maxResults</i> value. For example:<br>
<br>
<pre><code>   ...?firstResult=0&amp;maxResults=20<br>
   ...?firstResult=20&amp;maxResults=20<br>
   ...?firstResult=40&amp;maxResults=20<br>
   etc<br>
</code></pre>

If you don't want to show the whole results at once, this "pagination" method is very effective memory and speedwise.<br>
<br>
<br>
<h2>Some Examples</h2>

<ul><li>Getting the result for "brca2" in PSI-MITAB 2.5 format<br>
<blockquote><a href='http://www.ebi.ac.uk/Tools/webservices/psicquic/intact/webservices/current/search/query/brca2'>http://www.ebi.ac.uk/Tools/webservices/psicquic/intact/webservices/current/search/query/brca2</a></blockquote></li></ul>

<ul><li>The same, in PSI-MI XML 2.5.4 format<br>
<blockquote><a href='http://www.ebi.ac.uk/Tools/webservices/psicquic/intact/webservices/current/search/query/brca2?format=xml25'>http://www.ebi.ac.uk/Tools/webservices/psicquic/intact/webservices/current/search/query/brca2?format=xml25</a></blockquote></li></ul>

<ul><li>It supports paging. For instance, search for "species:human" and get only the first 100 results<br>
<blockquote><a href='http://www.ebi.ac.uk/Tools/webservices/psicquic/intact/webservices/current/search/query/species:human?firstResult=0&maxResults=100'>http://www.ebi.ac.uk/Tools/webservices/psicquic/intact/webservices/current/search/query/species:human?firstResult=0&amp;maxResults=100</a></blockquote></li></ul>

<ul><li>All of matrixdb in PSI-MITAB format<br>
<blockquote><a href='http://matrixdb.ibcp.fr:8080/webservices/current/search/query/*'>http://matrixdb.ibcp.fr:8080/webservices/current/search/query/*</a>