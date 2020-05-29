# Maven

    mvn archetype:generate -DgroupId=com.vj.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false 
    
    mvn clean
    mvn install
    mvn install -DskipTests
    java -cp target/my-app-1.0-SNAPSHOT.jar com.vj.app.App
    
    
# mvn pluginId:goalId
    mvn install:install
    mvn archetype:generate
    mvn dependency:tree -Dverbose
    mvn dependency:tree -Dverbose -Dincludes=commons-collections


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

# dependency Scope
- compile time scope (default scope)
- provided ,  ex: servlet-api  , no need to be exported 
- runtime 
- test , needed only during test
- system , <systemPath>${basedir}\lib\external.jar</systemPath>
- import 
    
# Portability ( using Profiles)

    src/main/profiles
    |-dev
      |- application.properties
            db.url=dev-url
    |-prod
      |- application.properties
            db.url=prod-url
    |-uat
      |- application.properties
            db.url=uat-url
    
   ------ 
   pom.xml

    
    <profiles>
        <profile>
            <id>dev</id>
            <properties>
                <build.profile.id>dev</build.profile.id>
            </properties>
            <build>
                <resouces>
                    <directory>src/main/profiles/dev</directory>
                </resources>
            </build>
        </profile>
        <profile>
            <id>prod</id>
            <properties>
                <build.profile.id>prod</build.profile.id>
            </properties>
            <build>
                <resouces>
                    <directory>src/main/profiles/prod</directory>
                </resources>
            </build>
        </profile>
        <profile>
            <id>uat</id>
            <properties>
                <build.profile.id>uat</build.profile.id>
            </properties>
            <build>
                <resouces>
                    <directory>src/main/profiles/uat</directory>
                </resources>
            </build>
        </profile>
    </profiles>
    
# selecting  profile

    mvn install -pdev
or

project properties > maven > Active Maven profile > dev > apply > yes 
build

 [ To Verify ] - target/app/jar --> unzip --> contains dev related application.propeties



# Java 1.8  & Main Class

    <plugins>
          <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
              <source>1.8</source>
              <target>1.8</target>
            </configuration>
          </plugin>
         
          <plugin>
            <artifactId>maven-jar-plugin</artifactId>
            <version>3.0.2</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
                <archive>
                    <manifest>
                        <mainClass>com.vj.app.Main</mainClass>
                    </manifest>
                </archive>
            </configuration>
         </plugin>
     </plugins>
     
# Junit

    <!-- https://mvnrepository.com/artifact/junit/junit -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.4</version>
        <scope>test</scope>
    </dependency>

     
 # Developer Info 
 
     <developers>
            <developer>
                <id>VijayRamisetty</id>
                <name>Vijaya Kumar Ramisetty</name>
                <email>ramisetty.v@outlook.com</email>
                <organization>MyOrganization</organization>
                <roles>
                    <role>Developer</role>
                </roles>
            </developer>
        </developers>
        
        
  # for web application
  -  -DarchetypeArtifactId= **maven-archetype-webapp**
  - servlet geronimo maven dependency required 
  
  # Multi Module Project 
  
    productparent folder  
       |- pom.xml      <---- parent pom.xml
       |- productservices 
           |- pom.xml  <---- child1 pom.xml
       |- productweb      
           |- pom.xml  <---- child2 pom.xml
           
  # Parent ( pom.xml ) 
  
      <project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        
        <groupId>com.vj.spark</groupId>
        <artifactId>productparent</artifactId>
        <version>1.0</version>
        <packaging>pom</packaging>
        
        <name>productparent</name>
        <url>http://maven.apache.org</url>
        
        <properties>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        </properties>
    
        <modules>
            <module>productservices</module>
            <module>productweb</module>
        </modules>
        
  # productservices (pom.xml)
     <project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
    
     <parent>
        <groupId>com.vj.spark</groupId>
        <artifactId>productparent</artifactId>
        <version>1.0</version>
      </parent> 
      
      <artifactId>productservices</artifactId>
      <packaging>jar</packaging>
      
       <name>productservices</name>
       <url>http://maven.apache.org</url>
        
 # productweb (pom.xml)
      <project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
         <modelVersion>4.0.0</modelVersion>
     
      <parent>
         <groupId>com.vj.spark</groupId>
         <artifactId>productparent</artifactId>
         <version>1.0</version>
       </parent> 
       
       <artifactId>productweb</artifactId>
       <packaging>war</packaging>
       
        <name>productweb</name>
        <url>http://maven.apache.org</url>
        
# Building Multi Module Project 

    cd parent
    mvn install 
 
 
  