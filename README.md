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

```sh
mvn clean install -Dparameter.gpg.skip=false
```
