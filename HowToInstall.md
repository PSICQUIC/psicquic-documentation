# Installation #

This instructions are aimed to those who want to have its local instance of the PSICQUIC web service.

## Requirements ##

  * JAVA ([JDK 6](http://java.sun.com/javase/downloads/index.jsp))
  * [Maven 2](http://maven.apache.org)

## Obtaining the Reference Implementation source code ##
There are two ways to obtain the source code:

* From the download section, downloading [psicquic-ws-1.2.9 (.zip/.tar.gz)](https://github.com/PSICQUIC/psicquic-webservice/releases/tag/psicquic-ws-1.2.9) containing the sources
* Using a git client, clone the code

  `git clone https://github.com/PSICQUIC/psicquic-webservice.git`

# Creating an index #

The Reference Implementation uses a Lucene index to store the data. This index can be generated in many ways but for your convenience, a class to create it from a PSIMITAB file is included as part of the web service. The PSIMITAB format is described here and we recommend data providers to read the [Data Distribution Best Practices](DataDistributionBestPractices.md) as well as the [PSICQUIC FAQ](Faq.md) before starting to generate a PSIMITAB dataset.


This class can be executed using Maven:

```
cd psicquic-webservice
mvn clean compile -P createIndex -D psicquic.index=/path/to/new.index -D mitabFile=/path/to/mitab.txt -D hasHeader=true
```

Replace the **psicquic.index** (where the index will be created), **mitabFile** (mitab file to index) and **hasHeader** (whether the file has a header) values accordingly.

If for whatever reason this is not working to you, you can execute directly the class `uk.ac.ebi.intact.psicquic.ws.utils.MitabIndexer` that can be found in the psicquic-webservice project.

# Running the service #

You have two choices here:

## Starting the service locally, using Jetty ##

The web service project can be started with jetty directly. This is extremely useful when testing but can be used as well for production instances.

```
mvn clean jetty:run -D psicquic.index=/path/to/new.index
```

Use the **psicquic.index** created in the previous step.

From PSICQUIC Spec 1.1 it is possible to define and expose **properties** about the service. You can set which properties your service is going to show by passing the `psicquic.properties` variable. Properties are defined using `key=value` pairs, comma-separated and all the expression is quoted.

```
mvn clean jetty:run -D psicquic.index=/path/to/new.index -D psicquic.properties="owner=John Smith, contactinfo=My Address"
```

Here is a sample query listing a limited number of available interactions in  your local service:

```
http://localhost:9090/psicquic/webservices/current/search/query/*?firstResult=0&maxResults=10
```

## Using tomcat, or any other server ##

If the jetty hot launch does not work for you, you can package the application in a war file and deploy it in your favourite web server (e.g. Tomcat).
To create the war file with maven, use the following command:

```
mvn clean package -D psicquic.index=/path/to/new.index
```

Use the **psicquic.index** created in the index creation step. Make sure that you are using the full path to the index as othwerwise the web server would not find it. Once the command is run, you can find the war file in the `target` folder. Grab it and deploy it in any web server.

You can define **properties** as explained in the previous section:

```
mvn clean package -D psicquic.index=/path/to/new.index -D psicquic.properties="owner=John Smith, contactinfo=My Address"
```