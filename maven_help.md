# Maven

    mvn archetype:generate -DgroupId=com.vj.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false 
    
    mvn clean
    mvn install
    
    java -cp target/my-app-1.0-SNAPSHOT.jar com.vj.app.App
    
    
# mvn pluginId:goalId
    mvn install:install
    mvn archetype:generate

# mvn phase 
    mvn clean
    mvn compile
    mvn test
    mvn install

# Life Cycle Phases

    mvn install 
    
    phase                   Goal
    -----                   ----
    - process-resources     resources:resources
    - compile               compiler:compiler
    - test                  surefire:test
    - package               jar:jar  / war:war
    
# Maven Coordinates
- groupId
- artifactId
- version
- packaging
# Jar Name
    artifactId-version.packaging
# Maven Repositories
-   Maven Central Repository = https://repo.maven.apache.org/maven2/
-   Enterprise Repository  = runs on localserver for an organization
-   Local Repository = ~/.m2/repository

