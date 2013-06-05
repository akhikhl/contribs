#contribs

##Overview

Batch installation/deployment of all poms, jars and, optionally, sources 
and javadoc from the current folder (and all it's subfolders)
to the local maven repository.

This is gradle script. It is supposed to be run from command line.

To learn what is gradle look here: http://www.gradle.org/

The script supports two tasks: installContribs and cleanContribs.

The script can be extended with other tasks, for example, for deploying
to company-wide artifactory etc.

##installContribs task

###Usage

```shell
gradle -b contribs.gradle
```
or
```shell
gradle installContribs -b contribs.gradle
```

###Effect

This task iterates the current folder (where "contribs.gradle" resides) and all it's subfolders,
in each folder it iterates files with extension "pom", for each found file
it looks for ".jar", "-sources.jar" and "-javadoc.jar" and install all found files
to the local maven repository.

The script accurately calculates inputs/outputs. If all files were already installed,
it does not install anything and shows "UP-TO-DATE" in the console.

The timestamp of last artifact installation is saved into file "build/contribsInstalled".

##cleanContribs task

###Usage

```shell
gradle cleanContribs -b contribs.gradle
```

###Effect

Removes "build" folder, so that script "forgets" about the time of the last artifact installation.
As the result, running script with installContribs task will install all artifacts anew.

The script accurately calculates inputs/outputs. "build" folder was already removed,
it does not remove any files/folders and shows "UP-TO-DATE" in the console.

##Copyright and License

Copyright 2013 (c) Andrey Hihlovskiy

All versions, present and past, of contribs script are licensed under MIT license:

* [MIT](http://opensource.org/licenses/MIT)
