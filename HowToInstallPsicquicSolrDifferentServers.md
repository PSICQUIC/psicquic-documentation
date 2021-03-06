# Installation

This instructions are aimed to those who want to have its local instance of the PSICQUIC web service based on SOLR.

# Requirements

* JAVA \([JDK 6](http://java.sun.com/javase/downloads/index.jsp)\)
* [Maven 2 or 3 \(3 is recommended\)](http://maven.apache.org)
* [SOLR 3.6.2](http://archive.apache.org/dist/lucene/solr/3.6.2/)

# Installing solr and solr-home

## Obtaining the solr schema used in the reference implementation

* Clone the code :

    `git clone https://github.com/PSICQUIC/psicquic-solr.git`

* Copy solr-home directory (psicquic-solr/src/main/resources/solr-home/) in your solr working directory:

    `cp -r psicquic-solr/src/main/resources/solr-home/ path/to/your/solr-workingdir`

## Starting solr server

The solr.war file is available in `psicquic-solr/src/main/resources/solr.war` or you can download the solr 3.6.2 package from apache website [http://archive.apache.org/dist/lucene/solr/3.6.2/](http://archive.apache.org/dist/lucene/solr/3.6.2/)

In the environment of your solr server, it is important to set the variable `solr.solr.home` which will point to the solr-home folder that you copied in your system. More information about how to install solr is available here [http://wiki.apache.org/solr/SolrInstall](http://wiki.apache.org/solr/SolrInstall)

# Obtaining the Reference Implementation source code

There are two ways to obtain the source code:

* Download the [psicquic-solr-ws-1.4.0.zip](https://github.com/PSICQUIC/psicquic-solr-ws/releases/tag/psicquic-solr-ws-1.4.0)

* Using a git client, clone the code

  `git clone https://github.com/PSICQUIC/psicquic-solr-ws.git`


# Building the index

The Reference Implementation uses SOLR (based on LUCENE) to index the data. This index can be generated in many ways but for your convenience, a class to create it from a PSIMITAB files (versions 2.5, 2.6, 2.7 and 2.8 are supported) is included as part of the web service. The PSIMITAB formats are described in [MITAB25Format](MITAB25Format.md), [MITAB26Format](MITAB26Format.md), [MITAB27Format](MITAB27Format.md), [MITAB28Format](MITAB28Format.md) and we recommend data providers to read the [Data Distribution Best Practices](DataDistributionBestPractices.md) as well as the [PSICQUIC FAQ](Faq.md) before starting to generate a PSIMITAB dataset.

## Creating an index

When the indexing job starts, it creates a file _target/mitabIndexJob\_currentTimeMillis_ which contains the job ID of the indexing process. This job ID will be necessary if you want to restart the indexing process from where it failed in case of a badly formatted MITAB line for instance.

  * You can run this bash script:

  ```
  cd psicquic-solr-ws
  bash indexMitabWithSolrUrl.sh /path/to/mitab-file solr-server-url
  ```

  where

    * **/path/to/mitab-file** is the path to the MITAB file to index. This argument is mandatory.
    * **solr-server-url** is the URL of your solr server. By default if not provided, it is [http://localhost:9090/solr/](http://localhost:9090/solr/). 


  * The indexing can be executed using the Maven command (used by the bash script):

  ```
  cd psicquic-solr-ws
  mvn clean install -PcreateIndexWithSolrRunning -DmitabFile=/path/to/mitab-file -DsolrUrl=solr-server-url -Dmaven.test.skip
  ```

  where

    * **/path/to/mitab-file** is the path to the MITAB file to index. This argument is mandatory.
    * **solr-server-url** is the URL of your solr server. By default if not provided, it is [http://localhost:9090/solr/](http://localhost:9090/solr/).

## Restarting the indexing process where it failed \(in case it failed\)

It can happen that the indexing process fails (bad formatted MITAB line for instance, solr server down, etc.). In this case you may want to restart the indexing process from where it failed (after fixing the badly formatted line for instance). Look at the job ID in the file target/mitabIndexJob_currentTimeMillis and then you have two ways of restarting the indexing:

  * You can run this bash script :

  ```
  cd psicquic-solr-ws
  bash restartIndexMitabWithSolrUrl.sh /path/to/mitab-file job-ID solr-server-url
  ```

  where

    * **/path/to/mitab-file** is the path to the MITAB file to index. This argument is mandatory.
    * **job-ID** is the job ID in the file target/mitabIndexJob_currentTimeMillis generated by the indexing script that failed. This argument is mandatory.
    * **solr-server-url** is the URL of your solr server. By default if not provided, it is [http://localhost:9090/solr/](http://localhost:9090/solr/).


  * The script can be executed using the Maven command (used by the bash script) :

  ```
  cd psicquic-solr-ws
  mvn install -PrestartIndexWithSolrRunning -Dmitab.file=/path/to/mitab-file -DsolrUrl=solr-server-url -Dindexing.id=job-ID -Dmaven.test.skip
  ```

  where

    * **/path/to/mitab-file** is the path to the MITAB file to index. This argument is mandatory.
    * **job-ID** is the job ID in the file target/mitabIndexJob_currentTimeMillis generated by the indexing script that failed. This argument is mandatory.
    * **solr-server-url** is the URL of your solr server. By default if not provided, it is [http://localhost:9090/solr/](http://localhost:9090/solr/).

# Starting the PSICQUIC service locally

## Starting with jetty

You can use jetty to start the psicquic service (good for testing but can be used in production as well)

  * You can run this bash script :

  ```
  cd psicquic-solr-ws
  bash startPsicquicServerOnly.sh solr-server-url
  ```
  where
   
    * **solr-server-url** is the URL of your solr server. By default if not provided, it is [http://localhost:9090/solr/](http://localhost:9090/solr/).


  * The PSICQUIC service and solr can be started using the Maven command (used by the bash script) :

  ```
  cd psicquic-solr-ws
  mvn clean jetty:run -Dmaven.test.skip -DsolrUrl=solr-server-url
  ```

  where

    * **solr-server-url** is the URL of your solr server. By default if not provided, it is [http://localhost:9090/solr/](http://localhost:9090/solr/).

Note that if you get an error like **Address already in use**, then you have to setup the solr server on a different port than 9090 (which is used by default by the psicquic service).

From PSICQUIC Spec 1.1 it is possible to define and expose **properties** about the service. You can set which properties your service is going to show by passing the `psicquic.properties` variable. Properties are defined using `key=value` pairs, comma-separated and all the expression is quoted.

```
mvn clean jetty:run -Dmaven.test.skip -DsolrUrl=solr-server-url -D psicquic.properties="owner=John Smith, contactinfo=My Address"
```

If you decide to use maven command, other parameters can be configured :

* -Djetty.port=9090
* -Dsolr.host=127.0.0.1 to set up the virtual host for solr admin interface. By default is private only
* -Dpsicquic.properties=properties-file-name
* -Dpsicquic.filter=filter-query (define some filters for your service)
* -Dservice.name=name (the name of the service such as intact, mint, ... which will be used to create the war file). If no service name is provided, the default name is 'default'
* -Dlog.file.name=filename (define a log file where you want to log all the queries that have been sent to your service)

## Using tomcat, or any other server

If the jetty hot launch does not work for you, you can package the application in a war file and deploy it in your favourite web server (e.g. Tomcat).
To create the war file with maven, use the following command:

```
mvn clean package -DsolrUrl=solr-server-url
```

where

* **solr-server-url** is the URL of your solr server. By default if not provided, it is [http://localhost:9090/solr/](http://localhost:9090/solr/).

Here is a sample query listing a limited number of available interactions in  your local service:

```
http://localhost:9090/psicquic/webservices/current/search/query/*?firstResult=0&maxResults=10
```

