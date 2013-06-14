#contribs

##Overview

Batch installation/deployment of all poms, jars and, optionally, sources 
and javadoc from the current folder (and all it's subfolders)
to the local or remote maven repository.

This is gradle script. It is supposed to be run from command line.

To learn what is gradle look here: http://www.gradle.org/

The script supports the following tasks: install, uploadArchives and clean.

##install task

###Usage

```shell
gradle install
```

###Effect

This task iterates the current folder (where "build.gradle" resides) and all it's subfolders,
in each folder it iterates files with extension "pom", for each found file
it looks for ".jar", "-sources.jar" and "-javadoc.jar" and installs all found files
to the local maven repository.

This task accurately calculates inputs/outputs. If all files were already installed,
it does not install anything and shows "UP-TO-DATE" in the console.

The timestamp of last artifact installation is saved into file "build/contribsInstalled".

##uploadArchives task

###Usage

```shell
gradle uploadArchives
```

###Effect

This task iterates the current folder (where "build.gradle" resides) and all it's subfolders,
in each folder it iterates files with extension "pom", for each found file
it looks for ".jar", "-sources.jar" and "-javadoc.jar" and installs all found files
to the network-accessible maven repository.

This task always uploads artifacts to maven-repository. No comparison to previously
uploaded artifacts is done.

**Attention**

"uploadArchives" task requires root project to define the following structure:

```groovy
rootProject {
  ext.corporateDeployment = [ url: "http://someurl", user: "someUser", password : "somePassword" ]
}
```

"corporateDeployment" could be placed to "build.gradle" at the root of project tree.
Much better solution would be to place it to gradle initialization script 
outside of project (for example, to "$HOME/.gradle/init.d/someGradleScript.gradle"),
so that sources stay clear of any environment-specific settings.

##clean task

###Usage

```shell
gradle clean
```

###Effect

Removes "build" folder, so that script "forgets" about the time of the last artifact installation.
As the result, running "gradle install" task will install all artifacts anew.

This task accurately calculates inputs/outputs. "build" folder was already removed,
it does not remove any files/folders and shows "UP-TO-DATE" in the console.

##Copyright and License

Copyright 2013 (c) Andrey Hihlovskiy

All versions, present and past, of contribs script are licensed under MIT license:

* [MIT](http://opensource.org/licenses/MIT)
