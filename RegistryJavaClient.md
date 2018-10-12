# Introduction #

This page explains how to access the Registry using the provided Java client. If you want to query a PSICQUIC service with Java, check [this page](JavaClient.md) instead.

# Getting the client #

You can download the latest client release version [here](https://www.ebi.ac.uk/Tools/maven/repos/content/groups/ebi-repo/org/hupo/psi/mi/psicquic/psicquic-registry-client/), or use this Maven dependency in your project:

```
    <dependency>
        <groupId>org.hupo.psi.mi.psicquic</groupId>
        <artifactId>psicquic-registry-client</artifactId>
        <version>1.4.0</version>
    </dependency>
```
This dependency is hosted at the European Bioinformatics Institute (EBI) repository. You can add this repository in your `pom.xml` file like this:

```
    <repositories>
        <repository>
            <id>nexus-ebi-release-repo</id>
            <url>http://www.ebi.ac.uk/Tools/maven/repos/content/groups/ebi-repo/</url>
        </repository>
    </repositories>
```

# Usage #

```
PsicquicRegistryClient registryClient = new DefaultPsicquicRegistryClient();

List<ServiceType> services = registryClient.listServices();

for (ServiceType service : services) {
    System.out.println(service.getName());
}
```

# Examples #

For an implementation of the example above see [here](https://github.com/PSICQUIC/psicquic-registry-client/blob/master/src/main/java/org/hupo/psi/mi/psicquic/registry/client/registry/DefaultPsicquicRegistryClient.java).