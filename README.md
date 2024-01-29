
Welcome to the YAVI Java API

## WHAT IS YAVI JAVA API?
It is a fork of the VI Java API which is a set of Java libraries that aim to ease the usage of VI 
SDK Web Services interfaces. It's now open-sourced under a mixed BSD license and Apache-2.0 license.

It provides the following benefits to the Java developers:
* Enables OO programming with a well defined managed object model
* Reduces the need to use ManagedObjectReference and makes possible 
  compile time type checking
* Hides the complexity of the PropertyCollector
* Provides necessary utility classes to simplify VI SDK web interfaces
* High performance with 4+ times faster than AXIS engine
* Adds the ability to provide your own HTTP Client
* Adds logging using log4j
* Adds gradle support for the build system

As a result, the application code using this API is much shorter (70% less) 
and much more readable than the equivalent using web service interfaces 
directly. The API itself is straight-forward and easy to learn and use. 

## WHO CREATED THE API?
To find out more about the original VI Java API see http://vijava.sf.net

As for who created the fork called YAVI Java that is Michael Rice.

## Whats with the name?

The name YAVI means simply Yet Another VI Java. I forked this project and moved it to 
github because the project seemd stale and I felt it needed new life. I wanted things 
like GitHub, custom http clients, and logging, and tests as well as other stuff so I decided to 
fork the project and do it.

## What is this fork about 
This fork was created to cooperate with the Jakarta XML Bind API and Java 11. 


## Do I have to change my code to use this?

No!! This is a drop in replacement and requires no code modification, but does introduce some new
dependencies (Always check the build.gradle for the latest requirements):

    dependencies {
        implementation 'org.apache.directory.studio:org.dom4j.dom4j:1.6.1'
        implementation 'log4j:log4j:1.2.17'
        implementation 'org.apache.httpcomponents:httpclient:4.3.5'
        implementation 'jakarta.xml.bind:jakarta.xml.bind-api:4.0.1'
        compileOnly 'org.projectlombok:lombok:1.18.30'
        annotationProcessor 'org.projectlombok:lombok:1.18.30'    
        testImplementation 'javax.servlet:javax.servlet-api:3.1.0'
        testImplementation 'junit:junit-dep:4.11'
        testImplementation 'junit:junit:4.12'
        testImplementation 'org.spockframework:spock-core:0.7-groovy-2.0'
        testImplementation 'cglib:cglib-nodep:3.1'
        testImplementation 'org.objenesis:objenesis:2.1'
    }


## WHERE CAN I GET HELP?
File a bug: https://github.com/yavijava/yavijava/issues

IRC: Freenode IRC #vijava 

COPYRIGHT & LICENSE:
BSD. See the License.txt file for details


## What happened to the samples?!?!

Never fear. I removed them from the core of the project and made them their own project. They can be found here: https://github.com/yavijava/yavijava-samples


## Testing

Testing is broken into two main packages which are discussed below. It is very important that pull requests you send include a test. 
Many very large enterprise customers depend on this library so extensive work is being put into trying to cover as much of the codebase 
as possible with tests.

### Integration

The first package is integration tests which are stored in src/intTest There is a properties file included that contains the URL, 
username and password for use in connecting to a vCenter or HostSystem. It has a  default value of https://vcsa/sdk for its URL, 
and 'administrator@vsphere.local' for the user name, and 'password' is used for the default password. The reason these defaults 
are included is because I use the vCenter Server Appliance in SIM mode to do as many of the tests as possible and I create an 
alias in my /etc/hosts file so vcsa always points at my local vCenter. Next I use a very basic shell script to configure the VCSA 
SIM and use 'password' for my default password. To run these tests make sure the properties file contains valid information for your
environment. Next from the project root where the build.gradle is execute ```gradle intTest``` or use the gradlew script and execute: 
```./gradlew intTest```

### Unit

The Second package is the unit tests. These tests are stored in src/test These are basic unit tests and should be created using either
junit or spock. Tests can be written in pure Java or Groovy. Please use the appropriate folder for the language you create your test with. 
The unit tests are run automatically by travis-ci when a pull request is opened, and they should always be run before you open a pull request 
where you are introducing changes that either fix bugs, or add functionality to ensure they continue to pass with your changes. To run these 
tests execute ```gradle test``` or use the gradlew script and execute ```./gradlew test```
