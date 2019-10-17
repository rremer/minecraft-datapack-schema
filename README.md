# minecraft-datapack-schema

[![Build Status](https://img.shields.io/travis/rremer/minecraft-datapack-schema)](https://travis-ci.org/rremer/minecraft-datapack-schema)
[![Site](https://img.shields.io/badge/site-1.13.2-2-green.svg)](https://rremer.github.io/minecraft-datapack-schema/1.13.2-2/index.html)
[![Maven Central](https://img.shields.io/nexus/r/com.github.rremer/minecraft-datapack-schema?server=https%3A%2F%2Foss.sonatype.org)](https://search.maven.org/artifact/com.github.rremer/minecraft-datapack-schema/1.13.2-2/jar)
[![License](https://img.shields.io/github/license/rremer/minecraft-datapack-schema)](https://opensource.org/licenses/MIT)
[![Keybase PGP](https://img.shields.io/keybase/pgp/rremer)](https://keybase.io/rremer/pgp_keys.asc)

Schema for Minecraft Datapacks.

## Usage

In your maven project with oss.sonatype.org as an upstream repository, point at the schema and and add a ```<validation>``` for each type of resource you have. There are currently schemas for [advancement], [loot_table], [recipe], [tag], or [mcmeta]:

```xml
  <properties>
    <version.json-schema-validator>1.2.0</version.json-schema-validator>
    <schema.url>https://rremer.github.io/minecraft-datapack-schema/1.13.2-2</schema.url>
  </properties>

  <build>
    <plugins>
      <plugin>
        <groupId>com.groupon.maven.plugin.json</groupId>
        <artifactId>json-schema-validator</artifactId>
        <version>${version.json-schema-validator}</version>
        <executions>
          <execution>
            <phase>test</phase>
            <goals>
              <goal>validate</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <validations>
            <validation>
              <directory>${project.basedir}/src/main/resources/recipes</directory>
              <jsonSchema>${schema.url}/recipe.schema.json</jsonSchema>
              <includes>
                <include>**/*.json</include>
              </includes>
            </validation>
          </validations>
        </configuration>
      </plugin>
    </plugins>
  </build>
```

## Building

```sh
mvn clean install
```

## Releasing

```sh
mvn versions:set -DnewVersion=1.13.2-2
mvn clean deploy -Dparameter.gpg.skip=false
mvn site site-deploy
```

### Versioning

A version number of this project's artifacts is built as ```<minecraft.version>-<project.version>```, where:
* ```minecraft.version``` is a version of minecraft (1.13.2, 1.14.4, ...)
* ```project.version``` is an increment for this project to release against a version of minecraft (1,2,3, ...)

[per their instructions]:https://central.sonatype.org/pages/apache-maven.html
[advancement]:https://rremer.github.io/minecraft-datapack-schema/1.13.2-2/advancement.schema.json
[loot_table]:https://rremer.github.io/minecraft-datapack-schema/1.13.2-2/loot_table.schema.json
[recipe]:https://rremer.github.io/minecraft-datapack-schema/1.13.2-2/recipe.schema.json
[tag]:https://rremer.github.io/minecraft-datapack-schema/1.13.2-2/tag.schema.json
[mcmeta]:https://rremer.github.io/minecraft-datapack-schema/1.13.2-2/mcmeta.schema.json
