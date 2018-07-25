# Java clients #

There are two JAVA clients provided by the project at the moment:

  * **PSICQUIC Simple Client**: it does not have dependencies. Provides basic access to the services by retrieving the raw data. It does not parse the results. It is REST based.
  * **PSICQUIC Client**: it has more dependencies, because it contains different models to manipulate the results in a Java object oriented way. At the moment it uses SOAP access, but this will be soon replaced to use the Simple Client behind the scenes soon.

You can download the clients [here](https://www.ebi.ac.uk/Tools/maven/repos/content/groups/ebi-repo/org/hupo/psi/mi/psicquic/), or obtain them using Maven.

The following table summarises the differences between the two clients, described in more detail below:

| **PSICQUIC Client** | **Simple**	| **Universal** |
|:--------------------|:-----------|:--------------|
| **Java lib dependencies**	| None	| Many |
| **Protocol used**	| REST	| SOAP |
| **Streaming**	| Yes	| No |
| **Pagination**	| Yes	| Yes |
| **Integration with model**	| None (but easily integrated)	| Full integration with XML and MITAB models |
| **Speed**	| Faster	| Slower (due to response generation) |
| **Bandwidth**	| Smaller	| Larger (SOAP evelope and response) |
| **Compression**	| Yes	| Yes |
| **Compatibility**	| PSICQUIC 1.1 or higher	| PSICQUIC 1.0 or higher |

## PSICQUIC Simple Client ##

This client is the simplest way to access the services using Java. It provides no-frills access to the data, hence it is quicker than the other client. You need to parse the results yourself though.

If you are using Maven, include the following in your project:

  * Latest release version (recommended)

```
      <dependency>
          <groupId>org.hupo.psi.mi.psicquic</groupId>
          <artifactId>psicquic-simple-client</artifactId>
          <version>1.3.4</version>
      </dependency>
```

  * Current version under development

```
      <dependency>
          <groupId>org.hupo.psi.mi.psicquic</groupId>
          <artifactId>psicquic-simple-client</artifactId>
          <version>1.3.5-SNAPSHOT</version>
      </dependency>
```

As of now, this dependency is hosted at the European Bioinformatics Institute (EBI) repository. You can add this repository in your `pom.xml` file like this:

```
     <repositories>
        <repository>
            <id>nexus</id>
            <name>European Bioinformatics Institute</name>
            <url>http://www.ebi.ac.uk/intact/maven/nexus/content/groups/public</url>
        </repository>
    </repositories>
```

### Examples of Use ###

You can find different examples in [this folder](https://github.com/PSICQUIC/psicquic-simple-client/tree/master/src/example/java/org/hupo/psi/mi/psicquic/wsclient).

## PSICQUIC Client (Standard) ##

A JAVA client is provided already by this project. If your project is using [Maven 2](http://maven.apache.org),  you can start using the client right away just by adding this dependencies to your project.

Include the following dependency in your project:

  * Latest released version

```
      <dependency>
          <groupId>org.hupo.psi.mi.psicquic</groupId>
          <artifactId>psicquic-client</artifactId>
          <version>1.5.3</version>
      </dependency>
```

  * Current version under development

```
      <dependency>
          <groupId>org.hupo.psi.mi.psicquic</groupId>
          <artifactId>psicquic-client</artifactId>
          <version>1.5.4-SNAPSHOT</version>
      </dependency>
```

As of now, this dependency is hosted at the European Bioinformatics Institute (EBI) repository. You can add this repository in your `pom.xml` file like this:

```
    <repositories>
        <repository>
            <id>intact.nexus</id>
            <name>IntAct Nexus</name>
            <url>http://www.ebi.ac.uk/intact/maven/nexus/content/groups/public</url>
        </repository>
    </repositories>
```

Examples on how to use the client can be found [here](https://github.com/PSICQUIC/psicquic-client/tree/master/src/example/java/org/hupo/psi/mi/psicquic/example).


### Examples of Use ###

You can use code like [this one](https://github.com/PSICQUIC/psicquic-client/tree/master/src/example/java/org/hupo/psi/mi/psicquic/example) to start using the PSICQUIC service.

### Building the client from sources ###

The sources for this client can be found as part of the [project source code](https://github.com/PSICQUIC/psicquic-client).

Once you have the code and you want to build the project, execute the Maven command:

```
cd psicquic-client
mvn clean install
```

# Using other programming languages #

If you are not using JAVA, you can generate your client code using the WSDL file directly. The WSDL can be found at:

  * version 1.0 : 
https://github.com/PSICQUIC/psicquic-solr-ws/blob/master/src/main/wsdl/psicquic10.wsdl
  * version 1.1 (recommended) : https://github.com/PSICQUIC/psicquic-solr-ws/blob/master/src/main/wsdl/psicquic11.wsdl