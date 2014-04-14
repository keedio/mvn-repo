Maven repository for dependencies not published in official Maven Repository

#USE

##Generate .pom and . jar

  - In pom.xml from the origin project include:

    \<distributionManagement\>  
      \<repository\>  
        \<id\>internal.repo\</id\>  
        \<name\>Temporary Staging Repository\</name\>  
        \<url\>file://${project.build.directory}/mvn-repo\</url\>  
      \</repository\>  
    \</distributionManagement\>  
    
    
    \<build\>  
     \<plugins\>  
      \<plugin\>  
        \<artifactId\>maven-deploy-plugin\</artifactId\>  
        \<version\>2.8.1\</version\>  
        \<configuration\>  
          \<altDeploymentRepository\>internal.repo::default::file://${project.build.directory}/mvn-repo\</altDeploymentRepository\>  
        \</configuration\>  
      \</plugin\>  
     \</plugins\>  
   \</build\>  

  - Execute mvn deploy  
  
  - Push the files generated (target/mvn-repo) in this git repository  
  
## Use our libs in other projects

  - Edit pom.xml  
  
     \<plugin\>  
        \<groupId\>org.apache.maven.plugins\</groupId\>  
        \<artifactId\>maven-dependency-plugin\</artifactId\>  
        \<version\>2.8\</version\>  
         \<executions\>  
            \<execution\>  
              \<id\>copy\</id\>  
              \<phase\>package\</phase\>  
              \<goals\>  
                \<goal\>copy\</goal\>  
              \</goals\>  
              \<configuration\>  
                \<artifactItems\>  
                  \<artifactItem\>  
                    \<groupId\>org.apache.avro\</groupId\>  
                    \<artifactId\>avro\</artifactId\>  
                    \<version\>1.7.4\</version\>  
                    \<type\>jar\</type\>  
                    \<overWrite\>false\</overWrite\>  
                    \<outputDirectory\>${project.build.directory}/libs\</outputDirectory\>  
                  \</artifactItem\>  
               \</artifactItems\>  
              \</configuration\>  
            \</execution\>  
          \</executions\>  
       \</plugin\>  

