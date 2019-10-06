# minecraft-datapack-schema

[![Build Status](https://travis-ci.org/rremer/minecraft-datapack-schema.svg?branch=master)](https://travis-ci.org/rremer/minecraft-datapack-schema)

Schema and parent for Minecraft Datapacks.

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
mvn versions:set -DnewVersion=1.0.1
mvn clean deploy -Dparameter.gpg.skip=false
```

[per their instructions]:https://central.sonatype.org/pages/apache-maven.html
