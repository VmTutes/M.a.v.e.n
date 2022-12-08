# Maven
VmTutes Maven
			
Maven Index
-----------
1. Overview of Maven  
2. Diff b/w Maven and Ant 
3. Diff b/w Maven and Other build tools  
4. How to install Maven in Windows
5. How to install Maven in Linux
6. Maven Architecture   
7. Maven Goles
8. Maven Life Cycle
9. Standard Directory Layout
10. GAV 
11. Maven local and remote repositories  
12. Packages and their types 
13. Sample Maven Project  
14. One by one goals executions
15. Build in and custom plugins
16. POM File
17. Maven SNAPSHORT
18. Maven profiles
19. Maven dependency   

Build Tool
----------

- Build :  is a process that we compile and assemble all the source code(written by developers) into object files.
		
Alternatives
------------
   
- Ant--> Apache Foundation product   
- Gradle--> Alternative for Maven   
- Maven--> latest and updated one 
- Grunt  
- Gulp 


Ant vs Maven
-------------
 - actions are defined in ant(so much of scripting) <<--------->>  in maven say what to do not how to do
 - sequences are defined in ant 		               <<--------->> how to build is defined in maven (life cycle)
 - no default directory structure   		               <<--------->> it fallows standard directory structure(default)
 - ant fallows you              		               <<--------->> you need to fallow maven
 - librarys are part of source code (difficult to maintain)    <<--------->> librarys are not part of source code
    	
Diff with other tools
---------------------
* open source
* it is not only build tool and also project management tool
* it has set of standards and object modules,so no need to instruct 	
* default project lifecycle 
* dependency management

What maven do?
--------------
- Compiling Source Code               
- Packaging Biniries/artifacts
- running Automated tests                         
- Deploying to production system
- Creating Documentation

Variables:
---------
-  Variables  :  variable is a name which holds/stores data. 
	- user  :  user defind variables eg:- vmtutes = Vinodh-Machireddy-Tutorials
	- system variables. :  Already created variables (or) pre-defind variables. eg:- echo $PATH, $HOME, $SHELL...etc

      Note:-  if we want to use variables globally   "export vmtutes = Vinodh-Machireddy-Tutorials" (in bashrc file)

Maven Installation in Windows:  
------------------------------
	@ install java above 7.1 version
	@ Download java JDK & JRE (or)  http://www.oracle.com/technetwork/java/javase/downloads/index.html
	@ Go to-->mycomputer-->properties-->Advanced system settings-->environment variables-->system variables
	@ path    ;C:\Program Files\Java\jdk1.8.0_131\bin;C:\Program Files\Java\jre1.8.0_131\bin;D:\Apache_Maven\bin  ---> to system variables PATH by seperater ;
	@ JAVA_HOME should point to JDK(without bin)
	@ install Maven
	@ Go to this website to downloab(Zip)--> maven.apache.org/download.cgi
		- D:\Apache_Maven ---> MAVEN_HOME in system variables
		- path--> ;D:\Apache_Maven\bin

maven installation in ec2
-------------------------
 1. Switch to root user
 
 		sudo -i  (or) sudo su - root 
 2. Update ec2 instance
 
	 	yum update -y 
3. Install java openjdk 

		yum install java-17-openjdk-devel -y
4. Go to optional folder in root directory to install maven 

		cd /opt
5. Download apache maven 

   		wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz
		
   note:- yum install wget -y (by default wget package will not install in redhat Linux)

6. unzip tarball
 
		tar xvzf apache-maven-3.8.6-bin.tar.gz
7. for permanent configuration

    	@  vi /etc/profile.d/maven.sh 
    	@  export MAVEN_HOME=/opt/apache-maven-3.8.6
    	@  export PATH=$PATH:$MAVEN_HOME/bin
    
8. give source where maven exists in the machine
 
		source /etc/profile.d/maven.sh
9. mvn --version

           o/p:- Apache Maven 3.8.6 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-17T19:33:14+01:00)
           	Maven home: /usr/local/src/apache-maven
           	Java version: 9.0.4, vendor: Oracle Corporation, runtime: /opt/java/jdk-9.0.4
           	Default locale: en_US, platform encoding: UTF-8
           	OS name: "linux", version: "4.17.6-1.el7.elrepo.x86_64", arch: "amd64", family: "unix"

verify whether java/maven is installed or not in CMD prompt by typing below commands

	- Javac --> compiler
	- java -->keyword
	- java -version --> runtime environment
	- mvn --version

How Maven works:(Architecture)
------------------------------
					       Build System
				       ---------------------------	
			              |			          |	      
	                Local Repo    |    POM.XML(conf file)     |  Remote Repo 		                                                  	      		
		      -------------->>|			          |<<----------------	(maintained by Maven opensource Community)
				      |		Maven	          |
				       ----------------------------
- it works as a GOALS, internally goals are plugins/jar files which has the future of when and what it has to do
	- eg:- maven test; --->>  then it will go and call test plugin to do testing
- remote maven repository located in - http://repo1.maven.org/maven2  (or) https://mvnrepository.com/
- local repo located in c:/user/machi --> .M2 --> Repository
- linux local repo in ls -a (.m2)

	
Dependency lifecycle:   
--------------------
	1. generate-source (.java files)
	2. compile -->all .java files into .class files(object files)
	3. test  ---> Unit test (a peace of code) 
	4. package --> deliveriable or executable or Artifacts(which contains all)
	5. install --> to convey info to maven local repo.(c:/user/vinodh --> .M2 --> Repository) 
        6. Deploy     
                           
	--> clean :- it deletes all runtime files
	--> site :- documentation(99% we will not use, very regularly for audits...)

Example Maven Goles:
--------------------
- mvn clean 
    - Invokes just clean

- mvn clean compile
    - Clean old builds and execute generate, compile

- mvn compile install
    - Invokes generate, compile, test, install
    
- mvn test clean
    - Invokes generate, compile, test then clean

Note:
diff source and binary code

1. source code which we can customize
2. binary code is a product which we can buy/use directly

Standard Directory Layout:
--------------------------
- if you want to work with maven project, then we need to follow the maven standard directory structure through which maven will work.
     - SRC
          - main : actual source code, lib files,additinal info, property files....etc
          - test : unit testing files
- once you start compile, maven will go to src/main folder to compile the code.

GAV:
----
- how maven identify which plugin to select when we instruct a goal. (G.A.V)
	- G(groupid) -- string rep company name / group name / business org on which u doing project.
	- A(artifactid) -- string rep product or deliverable(final output of your product)
	- V(versionid) -- Major.Minar.Patch/Maintanance( add SNAPSHOT to identify in development) 

Note:- How maven knows,where the source exists, what it has to do, where to keep output....etc, this all done by maven structure. 
 1. dir structure 
 2. pom.xml file

How you will get maven default structure
   - mvn archetype:generate
  
     note:- mvn -f pom.xml <goal>

Packages
--------
- jar - java archive(default package maven uses which contains group of .class files, so we group this to get a particular behaviour)
- war - web archive - contain group of jar + config + xml (for web based projects)
- ear - enterprice application

- packaging --> build type identified using the packaging element     
	eg : - pom ,jar(default),war,ear.    
 note: - by keeping pom in packaging it acts as a parent pom of all the modules


POM:(conf file)
---------------
Project object model is fundamental unit of work in maven,POM is an xml file that contains information about project and configuration
details used by maven to build project. pom conf file contains below list.

- Describe a project(meta data:- data about data)
- name and Version, Artifact type,source code location, Dependencies
- Plugins
- Profiles(Alternate build configuration)	
- it uses XML by default

Note:- atleast one pom.xml file should be there in product/project

Plugins:-
----------
if we want instruct anything to maven, through goals we will do, goals internally a plugins.
	
	1. Build Plugins : we will use this for entire life cycle
	2. Reporting Plugins : create documentation of product (for site phase only)

	    <build>
     		<plugins>
              	     <plugin>
	  		         1. GAV - how maven identifies plugins
	  		         2. when you have to run the plugin
	  	                 3. how to use plugin(like conn DB, insall, disconnect...etc)
	  		         4. what exactly to do
            	     </plugin>
   		    </plugins>
	    </build>
	
maven standared xml syntax for calling outside plugins:-
	
			<project>
			  <build> 
				<plugins> 
				  <plugin> 
				     <groupId>org.apache.maven.plugins</groupId>
				     <artifactId>maven-antrun-plugin</artifactId>
				     <version>1.1</version> 
				     <executions> 
				       <execution> 
					   <id>id.clean</id> 
					   <phase>clean</phase> 
					   <goals> 
					   <goal>run</goal>
					   </goals>
					   <configuration> 
					   <tasks> 
					      <echo>hallo world=============</echo> 
					   </tasks> 
					   </configuration>
				      </execution> 
				    </executions> 
				 </plugin> 
			       </plugins> 
			    </build>
			</project>

exec plugin to execute commands	
	
		<plugin>
			    <groupId>org.codehaus.mojo</groupId>
				<artifactId>exec-maven-plugin</artifactId>
				<version>1.6.0</version>
				<configuration>
				   <executable>mvn</executable>
					<arguments>--version</arguments>
				</configuration>		
		</plugin>

Note:- what plugin we selecting, what syntax(GAV) of plugin, And how to call....	
- maven ant plugin, maven exec plugin....

how to call a individual plugin:
---------------------------------
- mvn <GOAL> 
- mvn <PLUGIN>:<GOAL_NAME>
- mvn exec:exec
- mvn exec:java
- mvn <plugin>:<goal> ---> we can call plugin directly without phase/goal

SNAPSHOT:
--------
  1. it is under development build (or) dev copy which is not yet finalized(only we will change before releasing to client)
  2. other projects are depends on this, if i rebuild the jar name other proj looking for this

Maven Profile:
--------------
- def:- buid profile is a set of configurationns values which can be used to set or override dafault values of maven build.
        using a build profile, you can customize buid for different environments such as production v/s developmennt.

 - some times you want to execute only default plugins not all mentioned in build, at that time we can use.
	- mvn clean (default)
	- mvn -Pdemo  specify goal(all plugins)

		<profiles>
		       <profile>
			<id>demo</id>
				 <build>
				  </build>
		       </profile>
		</profiles>

- profile can activate many types like env, os, settings.xml in repo...etc

		<profile>  
		  <id>test</id>
		    <activation>
		       <property>    
		      <name>env</name>   
		       <value>test</value> 
		      </property>
		    </activation> 
		</profile>  

Dependency/Multy-Module Project:
--------------------------------

- if you have 1000 files in app.java project it is diffcult to maintain, so make modules/components like add, sub, dev of calculater project and copy src,pom file in each.
	
 note:- by keeping pom in packaging it acts as a parent pom of all modules (parent and child relationship)   demo (parent) > add, sub (childs)
	
		<modules>								
		       <module>add</module>
			<module>sub</module>
		</modules>

- Maven has 1st class multi-module support
- Each maven project creates 1 primary artifact
- A parent pom is used to group modules

issues -1:- 
 - executing all modules every time

overcome:- 
 - parent and child relationship, by keeping 'pom' file in "packaging"
	
		Ex:-

		  <groupId>EBU</groupId>
		  <artifactId>Parent-module</artifactId>
		  <version>1.0-SNAPSHOT</version>
		  <packaging>pom</packaging>
		    <modules>
			<module>Child-jar</module>
			<module>child-war</module>
		    </modules>

issue-2:-
- Dependencies
- adding add.jar to substration for dependency..

		<dependencies>
		    <dependency>
		      <groupId>training</groupId>
		      <artifactId>subtract</artifactId>
		      <version>1.0 SNAPSHORT</version>
		    </dependency>
		  </dependencies>

note:-
	
		<dependencies>				|
		    <dependency>			|
		      <groupId>junit</groupId>		|
		      <artifactId>junit</artifactId>	|------------>> junit plugin is default plugin for performing test phase
		      <version>3.8.1</version>		|
		      <scope>test</scope>		|
		    </dependency>			|
		  </dependencies>			|

- by using "install" phase in add module, then add.jar will move to local repo
- mvn install--> copying jar file form local project folder to local repository
- giving parent gav in child ==>>complete parent and child rel

Dependencys how maven know:
--------------------------
- if sub is depend on add file then we need to keep add file GAV into sub file dependency.
- error :- not able to find add file, then install add file from local project folder to local repository     
             -  mvn install



  		                                      ====THE END====       
			VmTutes, +91-7204143230(WhatsApp/Call), Email:- Vinodh-Machireddy@VmTutes.com















    


