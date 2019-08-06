# helloworld-maven-build-tool-example
Example of using Maven to create project directories
An Ant was created to overcome the shortages of make, 

 

Maven was created with a similar intention – to overcome the shortages of Ant. 

 

You may recall that make could not guarantee build portability because the commands make executes are arbitrary shell commands that may be system specific. 

 

An Ant build , if all tasks are available on the class path , is portable as long as Java runs the same way on the different platform. 

 

Developers realized that a significant effort of the projects utilizing And is devoted to project build tool configuration , including repetitive task. 

 

Maven approaches the build issue a bit differently.  

 

There are files that are needed for the operational code and these are files that contain some test code and data. 

 

Therefore we might have directories such as : 

 
```
   -src/test 

   -src/main 
```
 

Java files are in  
```
-/src/main/java 

-/src/test/java 
```
 

Resources files are under: 
```
-/src/main/resources 

-/src/test/resources 
```
 

What else would you like to with a Java project other than compile, test, package, or deploy it 

 

Maven defines these project life cycle for us. 

 

When we want to compile a project using Maven as a build tool, you will have to type $ mvn compile to compile the project. You can do that even before understanding what the project actually is. 

 

E.g. code: 

 
```
> mvn compile 
```
 

When we create a Maven project , we do not have to describe what the build process has to do and how it has to do it . We will have to describe the project , and only the parts that are project specific. 

 

The Build configuration of a Maven project is given in an XML file. 

 

The name of this file usually is  

 

**pom.xml** 

 

And that file should be in the root directory  when firing up Maven 

 

The **POM stands for Project Object Model**,  and it describes the projects in a hierarchical way. 

 

The source directories , the  packaging , and other things are define in a so-called super POM, which is part of the Maven Program. 

 

Anything that the POM defines , overrides the defaults defined in the super POM. 

 

The POMs are arranged into a hierarchy , and they inherit the configuration values from the parent down to the modules. 

 

##Installing Maven  

 

Maven is neither a part of the operating system nor the JDK. It has to be downloaded and installed in a very similar way to Ant. 

 

You can Download Maven from : 

 
```
                            https://maven.apache.org/ 
```
Under the download section , download the **tar.gz** format 

 

***It is very important to do a checksum test after you download the software. **

 

 

After the file is downloaded , you can explode it to a subdirectory using the following command: 

 
```
> tar xfz apache-maven-3.3.9-bin.tar.gz 
```
 

Then you should move the subdirectory to a usuabl binary distrubutinn of Maven to  

 
```
/bin/ 
```
 

Folder at root. 

 

After that you should add the system PATH 

 
```
> export M2_HOME=/bin/apache-maven-3.3.9/ 

> export PATH=${M2_HOME}bin:$PATH 
```
 

 

Using Maven 

Unlike Ant , Maven helps you create the skeleton of a new project. To do that use the following command: 

 
```
> mvn archetype:generate 
```
 

Maven will first download the actually available project types from the network and prompt you to select the one you want to use . Maven offers a default value when it asks for your choice , you can for now use the recommend default value. 
```
> Choose a number : 817 : 
```
 

After that , Maven will ask you for the version of the project 

 
```
      Choose a version 
```
 

If it is the first time creating the project choose 1.0 option number 5. 

 

The next thing Maven asks for is the groupID and the artifact ID of the project. 

 

E.g.: 

 
```
Define value for property 'groupID': : abolfazl.example.program 

Define value for property ;artifactId': : SortTutorial 
```
 

Next Maven asks for current version of the project. 

 
```
Define value for property 'version':: 1.0.0-SNAPSHOT 
```
 

Use semantic versioning  

Is a versioning scheme that suggests three digit version numbers M.m.p stands for Major.minor.patch 

Version numbers. This is very useful for libraries . You will increment the last version number if there is only a bug fixe since the previous release . You  will increment the minor number when the new release also contains new features, but the library is compatible with the previous version. 

 

The major release number is increased when the new version is significantly different from the previous one. 

 

Maven handles the versions that have the –SNAPSHOT  postfix as non-release versions. While we develop the code , we will have many versions of our code, all having the same snapshot version. On the other hand , non-snapshot version numbers can only be used only for a single version. 

 

The last question from the program skeleton generation is the name of the Java package. 

 

The default is the value we gave for groupID, and we will use this. It is a rare exception to use something else. 

 

E.g.: 

 
```
Define value for property 'package' : com.abolfazl_sadeghian.example.program 
```
 

After we have specified all the parameters that are needed , the final request is to confirm the settings. 

 

After entering  Y  , Maven will generate the files that are needed for the project and siplay the report. 

 

After that change to the directory with pom.xml  and type the following code to compile and run: 

 
```
> mvn package 

 ```

If you face an error add the following to the pom.xml file just above the dependencies: 

 

 ```

<url> … </url> 

…............................................................................................................................... 

<build> 

   <plugins>  

  

   <plugin> 

        <groupId>org.apache.maven.plugins</groupId> 

        <artifactId>maven-compiler-plugin</artifactId> 

        <configuration> 

            <source>1.9</source> 

            <target>1.9</target> 

        </configuration> 

    </plugin> 

  

   </plugins> 

  </build> 

…............................................................................................................................. 

<dependencies> 

… 

</dependencies> 

``` 

Maven fires up , compiles , and packages the project automatically.  

 

Maven compiles code with the default settings for Java version 1.5 . It means that the generate class file is compatible with Jave version 1.5 , and also that the complier only accepts language construct that were available already in Java 1.5. 

 

If we want to use newer language feature , we should edit the pom.xml file to contain the following lines. 

 

You can add the following code to use newer version of the Java Language: 

 
```
<build> 

  <plugins> 

    <plugin> 

      <groupId>org.apache.maven.plugins</groupId> 

      <artifactId>maven-compiler-plugin</artifactId> 

      <configuration> 

          <source>1.9</source> 

          <target>1.9</target> 

      </configuration> 

     </plugin> 

  </plugins> 

</build> 
```
 

Now you can start the code using the following command: 

 
```
> java –cp target/SortTutorial-1.0.0-SNAPSHOT.jar com.abolfazl_sadeghian.example.prorgram.App 
```
 
