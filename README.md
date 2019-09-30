# minecraft-datapack-schema

[![Build Status](https://travis-ci.org/rremer/minecraft-datapack-schema.svg?branch=master)](https://travis-ci.org/rremer/minecraft-datapack-schema)

Schema and parent for Minecraft Datapacks.

## Usage

In your maven project with oss.sonatype.org as an upstream repository:
```xml
  <parent>
    <groupId>com.github.rremer</groupId>
    <artifactId>minecraft-datapack-schema-parent</artifactId>
    <version>1.0.0-SNAPSHOT</version>
  </parent>

  <properties>
    <parameter.schema.validation.phase>test</parameter.schema.validation.phase>
  </properties>
```

## Building

```sh
mvn clean install
```

## Releasing

Ensure your gpg key is installed and ```settings.xml``` is updated with id oss.sonatype.org [per their instructions].

```sh
mvn versions:set -DnewVersion=1.0.1
mvn clean deploy -Dparameter.gpg.skip=false
```

[per their instructions]:https://central.sonatype.org/pages/apache-maven.html
