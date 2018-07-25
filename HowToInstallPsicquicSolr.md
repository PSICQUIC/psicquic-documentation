## PSICQUIC reference implementation based on SOLR (recommended) ##

The new PSICQUIC Reference Implementation is now based on SOLR which is an indexing software based on LUCENE. It can index MITAB 2.5, 2.6, 2.7 and 2.8 files.

You have two ways for building your psicquic webservice :

  * [How to install PSICQUIC using a single jetty server](HowToInstallPsicquicAndSolrJetty.md)
    * If you need to test quickly your webservice
    * If you want to start both the solr server and the PSICQUIC webservice using one single command line. However Both applications will be running on the same jetty server, which may not be what you want if you re-use your SOLR index/server for other applications -- eg -- when updating the solr server, it is better to leave the psiquic webservice running, this setup requires both to shut down at the same time.
  * [How to install PSICQUIC using a solr server independent from the PSICQUIC server](HowToInstallPsicquicSolrDifferentServers.md)
    * If you don't want to use jetty for running your PSICQUIC webservice
    * If you want to start the solr server in another server so you can reuse it in other applications independent from your PSICQUIC service
    * If you already have a solr server independent from the PSICQUIC server


