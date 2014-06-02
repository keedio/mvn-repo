Maven repository for dependencies not published in official Maven Repository

#USE

##Generate .pom and . jar

  - In pom.xml from the origin project include:
```
    <distributionManagement>  
      <repository>  
        <id>internal.repo</id>  
        <name>Temporary Staging Repository</name>  
        <url>file://${project.build.directory}/mvn-repo</url>  
      </repository>  
    </distributionManagement>  
    
    
    <build>  
     <plugins>  
      <plugin>  
        <artifactId>maven-deploy-plugin</artifactId>  
        <version>2.8.1</version>  
        <configuration>  
          <altDeploymentRepository>internal.repo::default::file://${project.build.directory}/mvn-repo</altDeploymentRepository>  
        </configuration>  
      </plugin>  
     </plugins>  
   <\build>  
```
  - Execute mvn deploy  
  
  - Push the files generated (target/mvn-repo) in this git repository  
  
## Use our libs in other projects

  - Edit pom.xml  
```
   <repositories>
    <repository>
      <id>my.mvn.repo</id>
      <url>https://github.com/mvalleavila/mvn-repo/raw/master</url>
      <!-- use snapshot version -->
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
    </repository>
  </repositories>
```

  Dependencies:
```    
    <dependency>
      <groupId>org.apache.avro.repo</groupId>
      <artifactId>avro-repo-bundle</artifactId>
      <version>1.7.4</version>
    </dependency>

```
