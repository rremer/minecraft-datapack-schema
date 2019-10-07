# minecraft-datapack-schema

[![Build Status](https://img.shields.io/travis/rremer/minecraft-datapack-schema)](https://travis-ci.org/rremer/minecraft-datapack-schema)
[![Maven Central](https://img.shields.io/nexus/r/com.github.rremer/minecraft-datapack-schema?server=https%3A%2F%2Foss.sonatype.org)](https://search.maven.org/artifact/com.github.rremer/minecraft-datapack-schema/1.13.2-1/jar)
[![License](https://img.shields.io/github/license/rremer/minecraft-datapack-schema)](https://opensource.org/licenses/MIT)
[![Keybase PGP](https://img.shields.io/keybase/pgp/rremer)](https://keybase.io/rremer/pgp_keys.asc)

Schema for Minecraft Datapacks.

## Usage

In your maven project with oss.sonatype.org as an upstream repository, unpack the schema jar and configure validations for each schema you implement:

```xml
  <properties>
    <version.json-schema-validator>1.2.0</version.json-schema-validator>
    <version.maven-dependency-plugin>3.1.1</version.maven-dependency-plugin>
    <version.minecraft-datapack-schema>1.13.2-1</version.minecraft-datapack-schema>
    <path.schema>${project.build.directory}/classes/schema</path.schema>
  </properties>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
        <version>${version.maven-dependency-plugin}</version>
        <executions>
          <execution>
            <id>unpack</id>
            <phase>process-test-resources</phase>
            <goals>
              <goal>unpack</goal>
            </goals>
            <configuration>
              <artifactItems>
                <artifact>
                  <groupId>com.github.rremer</groupId>
                  <artifactId>minecraft-datapack-schema</artifactId>
                  <version>${version.minecraft-datapack-schema}</version>
                </artifact>
              </artifactItems>
              <includes>**/*.schema</includes>
              <outputDirectory>${path.schema}</outputDirectory>
            </configuration>
          </execution>
        </executions>
      </plugin>
  <build>
    <plugins>
      <plugin>
        <groupId>com.groupon.maven.plugin.json</groupId>
        <artifactId>json-schema-validator</artifactId>
        <version>${version.minecraft-datapack-schema}</version>
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
              <directory>${project.basedir}/src/test/resources/advancements</directory>
              <jsonSchema>${path.schema}/advancement.schema</jsonSchema>
              <includes>
                <include>**/*.json</include>
              </includes>
            </validation>
            <validation>
              <directory>${project.basedir}/src/test/resources/recipes</directory>
              <jsonSchema>${path.schema}/recipe.schema</jsonSchema>
              <includes>
                <include>**/*.json</include>
              </includes>
            </validation>
            <validation>
              <directory>${project.basedir}/src/test/resources/loot_tables</directory>
              <jsonSchema>${path.schema}/loot_table.schema</jsonSchema>
              <includes>
                <include>**/*.json</include>
              </includes>
            </validation>
            <validation>
              <directory>${project.basedir}/src/test/resources/tags</directory>
              <jsonSchema>${path.schema}/tag.schema</jsonSchema>
              <includes>
                <include>**/*.json</include>
              </includes>
            </validation>
            <validation>
              <directory>${project.basedir}/src/test/resources/mcmeta</directory>
              <jsonSchema>${path.schema}/mcmeta.schema</jsonSchema>
              <includes>
                <include>**/*.mcmeta</include>
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

Ensure your gpg key is installed and ```settings.xml``` is updated with id oss.sonatype.org [per their instructions].

```sh
mvn versions:set -DnewVersion=1.13.2-2
mvn clean deploy -Dparameter.gpg.skip=false
```

### Versioning

A version number of this project's artifacts is built as ```<minecraft.version>-<project.version>```, where:
* ```minecraft.version``` is a version of minecraft (1.13.2, 1.14.4, ...)
* ```project.version``` is an increment for this project to release against a version of minecraft (1,2,3, ...)

[per their instructions]:https://central.sonatype.org/pages/apache-maven.html
