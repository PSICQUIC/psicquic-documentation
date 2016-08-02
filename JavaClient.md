

# Java clients #

There are two JAVA clients provided by the project at the moment:

  * **PSICQUIC Simple Client**: it does not have dependencies. Provides basic access to the services by retrieving the raw data. It does not parse the results. It is REST based.
  * **PSICQUIC Client**: it has more dependencies, because it contains different models to manipulate the results in a Java object oriented way. At the moment it uses SOAP access, but this will be soon replaced to use the Simple Client behind the scenes soon.

Both can be found in the [Downloads](http://code.google.com/p/psicquic/downloads/list) section, or obtained using Maven.

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
| **Compression**	| Available using specific format	| Yes |
| **Compatibility**	| PSICQUIC 1.1 or higher	| PSICQUIC 1.0 or higher |

## PSICQUIC Simple Client ##

This client is the simplest way to access the services using Java. It provides no-frills access to the data, hence it is quicker than the other client. You need to parse the results yourself though.

If you are using Maven, include the following in your project:

  * Latest release version (recommended)
```
<dependencies>
...

      <dependency>
          <groupId>org.hupo.psi.mi.psicquic</groupId>
          <artifactId>psicquic-simple-client</artifactId>
          <version>1.3.3</version>
      </dependency>

</dependencies>
```

  * Current version under development
```
<dependencies>
...

      <dependency>
          <groupId>org.hupo.psi.mi.psicquic</groupId>
          <artifactId>psicquic-simple-client</artifactId>
          <version>1.3.4-SNAPSHOT</version>
      </dependency>

</dependencies>
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

You can find different examples in [this folder](http://code.google.com/p/psicquic/source/browse/trunk/#trunk/psicquic-simple-client/src/example/java/org/hupo/psi/mi/psicquic/wsclient).

## PSICQUIC Client (Standard) ##

A JAVA client is provided already by this project. If your project is using [Maven 2](http://maven.apache.org),  you can start using the client right away just by adding this dependencies to your project.

Include the following dependency in your project:

  * Latest released version
```
<dependencies>
...

      <dependency>
          <groupId>org.hupo.psi.mi.psicquic</groupId>
          <artifactId>psicquic-client</artifactId>
          <version>1.5.3</version>
      </dependency>

</dependencies>
```

  * Current version under development
```
<dependencies>
...

      <dependency>
          <groupId>org.hupo.psi.mi.psicquic</groupId>
          <artifactId>psicquic-client</artifactId>
          <version>1.5.4-SNAPSHOT</version>
      </dependency>

</dependencies>
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

An example on how to use the client can be found [here](http://code.google.com/p/psicquic/source/browse/trunk/psicquic-client/src/example/java/org/hupo/psi/mi/psicquic/example/PsicquicClientExample.java).


### Examples of Use ###

You can use code like [this one](http://code.google.com/p/psicquic/source/browse/trunk/psicquic-client/src/example/java/org/hupo/psi/mi/psicquic/example/PsicquicClientExample.java) to start using the PSICQUIC service.

### Building the client from sources ###

The sources for this client can be found as part of the project source code. Follow the instructions in the [Source](http://code.google.com/p/psicquic/source/checkout) page to checkout the code.

Once you have the code, the client can be found in the `psicquic-client` folder. If you want to build the project, execute the Maven 2 command:

```
cd psicquic-client
mvn clean install
```

# Using other programing languages #

If you are not using JAVA, you can generate your client code using the WSDL file directly. The WSDL can be found at:

  * version 1.0
http://psicquic.googlecode.com/svn/trunk/psicquic-webservice/src/main/wsdl/psicquic10.wsdl
  * version 1.1 (recommended)
http://psicquic.googlecode.com/svn/trunk/psicquic-webservice/src/main/wsdl/psicquic11.wsdl