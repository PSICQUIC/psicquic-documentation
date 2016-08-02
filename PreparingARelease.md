# Introduction #

The PSICQUIC Reference Implementation will be released from time to time. This page contains the instructions to do it.


# Releasing the Reference Implementation #

When everyone is happy about releasing a new version of the Reference Implementation, this must be done:

  * Change the version in the POM file and commit the change.
  * Tag the project, running this command in the psicquic-ws folder.

```
mvn scm:tag -Dtag=psicquic-webservice-1.2.0
```

  * Create an assembly with the sources and upload the tar.gz bundle to the project, so it will be available as a download.

```
mvn clean assembly:assembly -DdescriptorId=src
```

  * Update the version of the project to the next SNAPSHOT version and commit.