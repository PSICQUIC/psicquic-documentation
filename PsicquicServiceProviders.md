# PSICQUIC Providers #

There are more than 30 PSICQUIC providers. As more molecular interaction databases implement PSICQUIC, this list of providers will grow.

It is possible to check dynamically on the status of each of this services by using the [Registry](http://www.ebi.ac.uk/Tools/webservices/psicquic/registry/registry?action=STATUS).

Notes:
  * Only those with version 1.0 or more support REST access.
  * Only those with version 1.2 or more support XGMML and RDF format.
  * Only those with version 1.3 or more support MITAB 2.7 and MITAB 2.6 format.
  * Only those with version 1.4 or more support the MITAB 2.8 format.
  * The webservices having a version inferior to 1.3 are based on [LUCENE](HowToInstallPsicquicLucene.md) reference implementation and the webservices having a version superior or equal to 1.3 are based on [SOLR](HowToInstallPsicquicSolr.md) reference implementation. The index is different but the data is the same.