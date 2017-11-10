# Introduction #

This page explains how to access the Registry using the provided Java client. If you want to query a PSICQUIC service with Java, check [this page](JavaClient.md) instead.

# Getting the client #

You can download the client and its dependencies in the [Downloads section](http://code.google.com/p/psicquic/downloads/list), or use this Maven dependency in your project:

  * Released versions
```
<dependency>
   <groupId>org.hupo.psi.mi.psicquic</groupId>
   <artifactId>psicquic-registry-client</artifactId>
   <version>1.1.1</version>
</dependency>
```

  * Current version under development
```
<dependency>
   <groupId>org.hupo.psi.mi.psicquic</groupId>
   <artifactId>psicquic-registry-client</artifactId>
   <version>1.1.2-SNAPSHOT</version>
</dependency>
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

Some examples can be found [here](http://code.google.com/p/intact/source/browse/repo#repo%2Fsite%2Ftrunk%2Fintact-course%2Fsrc%2Fmain%2Fjava%2Fintact%2Fsolution%2Fpsicquic%2Fregistry).