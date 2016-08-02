# Introduction #

This page presents a collection of Java programs that deal with PSICQUIC services and registry, while some of them only rely on a plain Java 5, some other require additional libraries.

# Code Samples #

## Samples that only require Java 5+ ##

**Example 1:** Listing active PSICQUIC services from the Registry: [code sample](http://code.google.com/p/intact/source/browse/repo/site/trunk/intact-kickstart/src/main/java/uk/ac/ebi/intact/kickstart/psicquic/QueryRegistry.java)

**Example 2:** Batch download of MITAB data from a PSICQUIC service: [code sample](http://code.google.com/p/intact/source/browse/repo/site/trunk/intact-kickstart/src/main/java/uk/ac/ebi/intact/kickstart/psicquic/DownloadBatchMITAB.java)


## Samples that use the PSICQUIC Simple Java Client ##

The Simple Java Client is the most performant way to access the data as it uses REST requests behind the scenes.

To try the examples, your require the PSICQUIC Simple Java library:

This goes in the dependencies section of your POM file wit other dependencies yo may require:
```
        <dependency>
            <groupId>org.hupo.psi.mi.psicquic</groupId>
            <artifactId>psicquic-simple-client</artifactId>
            <version>1.3.3</version>
        </dependency>
```

Alternatively, you can download the Simple Client from the Downloads section.

**Example 1:** Count and fetch data from a PSICQUIC service: [code sample](http://code.google.com/p/psicquic/source/browse/trunk/psicquic-simple-client/src/example/java/org/hupo/psi/mi/psicquic/wsclient/PsicquicSimpleExample.java)

**Example 2:** Count and fetch data from a PSICQUIC service, compressing the stream for faster transmission: [code sample](http://code.google.com/p/psicquic/source/browse/trunk/psicquic-simple-client/src/example/java/org/hupo/psi/mi/psicquic/wsclient/PsicquicSimpleExampleCompression.java)

In addition, it is possible to add the existing Java libraries to create an object model from the results. To do it, you will need to add these libraries to the classpath:

```
        <dependency>
            <groupId>psidev.psi.mi</groupId>
            <artifactId>psimitab</artifactId>
            <version>1.8.4</version>
            <scope>test</scope>
        </dependency>
         <dependency>
            <groupId>commons-logging</groupId>
            <artifactId>commons-logging</artifactId>
            <version>1.1.1</version>
            <scope>test</scope>
        </dependency>
```

Alternatively, download the psimitab library from the [psimi Google project](http://code.google.com/p/psimi/downloads/list).

**Example 3**: Parse the stream directly into a collection of `BinaryInteraction` objects. Be careful with this approach as it will store all the results in memory. It is useful for queries that do not return massive results (e.g. < 10,000 results).  [code sample](http://code.google.com/p/psicquic/source/browse/trunk/psicquic-simple-client/src/example/java/org/hupo/psi/mi/psicquic/wsclient/PsicquicSimpleMitabExample.java)

**Example 4**: Read line by line from the result stream and process one `BinaryInteraction` object at a time. [code sample](http://code.google.com/p/psicquic/source/browse/trunk/psicquic-simple-client/src/example/java/org/hupo/psi/mi/psicquic/wsclient/PsicquicSimpleMitabIterationExample.java)

## Samples that use the standard PSICQUIC Java Client ##

If you wish to run these samples you will have to add additional JAR files into your classpath, including the [Java client](JavaClient.md) and parsers for the standard formats. An easy way to do so is to use [Maven2](http://maven.apache.org/) and add the following into your POM file:

#### Dependency ####

This goes in the dependencies section of your POM file wit other dependencies yo may require:
```
        <dependency>
            <groupId>org.hupo.psi.mi.psicquic</groupId>
            <artifactId>psicquic-client</artifactId>
            <version>1.5.3</version>
        </dependency>
```

#### Maven Repository ####

This goes into the repositories section of your POM file:
```
            <repositories>
        <repository>
            <id>intact.nexus</id>
            <name>IntAct Nexus</name>
            <url>http://www.ebi.ac.uk/intact/maven/nexus/content/groups/public</url>
        </repository>
    </repositories>
```

**Example 1:** Read data from a single PSICQUIC service: [code sample](http://code.google.com/p/intact/source/browse/repo/site/trunk/intact-kickstart/src/main/java/uk/ac/ebi/intact/kickstart/psicquic/QuerySinglePsicquic.java)

**Example 2:** Read data from all active PSICQUIC services: [code sample](http://code.google.com/p/intact/source/browse/repo/site/trunk/intact-kickstart/src/main/java/uk/ac/ebi/intact/kickstart/psicquic/QueryMultiplePsicquic.java)