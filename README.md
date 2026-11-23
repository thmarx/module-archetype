# Condation CMS Module Archetype

This archetype creates a Maven multi-module project based on `example-module`,
with separate `api` and `module` artifacts and a distributable module ZIP.

## Install the archetype locally

From this directory, run:

```shell
mvn install
```

Run this step in the `module-archetype` directory, not in the empty directory
where you want to generate your module.

## Generate a module

After installing the archetype locally, run the following command from the
empty directory where you want the new project created. The fully qualified
plugin goal is intentional; it can run without a `pom.xml` in that directory.

### PowerShell

Pass the Maven arguments as an array so PowerShell forwards each argument
without reinterpreting it:

```powershell
$mavenArgs = @(
  'org.apache.maven.plugins:maven-archetype-plugin:3.4.1:generate'
  '-DarchetypeGroupId=com.condation.cms.modules'
  '-DarchetypeArtifactId=cms-module-archetype'
  '-DarchetypeVersion=1.0.0'
  '-DgroupId=com.example.cms.modules'
  '-DartifactId=my-module'
  '-Dversion=1.0.0'
  '-Dpackage=com.example.cms.modules.mymodule'
  '-DmoduleName=My module'
  '-DinteractiveMode=false'
  '-DarchetypeCatalog=local'
)
& mvn @mavenArgs
```

### CMD

```shell
mvn org.apache.maven.plugins:maven-archetype-plugin:3.4.1:generate -DarchetypeGroupId=com.condation.cms.modules -DarchetypeArtifactId=cms-module-archetype -DarchetypeVersion=1.0.0 -DgroupId=com.example.cms.modules -DartifactId=my-module -Dversion=1.0.0 -Dpackage=com.example.cms.modules.mymodule -DmoduleName="My module" -DinteractiveMode=false -DarchetypeCatalog=local
```

`moduleName` is used in the module metadata and the sample hook. If omitted in
interactive mode, it defaults to the artifact ID. The generated `module`
artifact ID and module ID use `artifactId`; the API artifact ID is
`artifactId-api`, and the parent artifact ID is `artifactId-parent`.

The generated project uses the CMS and modules framework versions from
`example-module`. Update those properties in the generated parent POM when
targeting different framework versions.

Build and package the generated module with:

```shell
cd my-module
mvn package
```

The distributable ZIP is created in `module/target`.
