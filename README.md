### **Maven Build Lifecycle**

* Maven is based on the concept of build life cycles.
* Now a lifecycle is going to be a predefined group of steps and these steps are called ***Phases***. 
* A lifecycle is a group of phases and each phase can be bound to one or more ***Plugin Goals***. 
* Any work that is done in Maven is going to be done by plugins. So basically the life cycle and phases provide a
framework for us to call plugin goals in a specific sequence. 

This is really how all Maven comes together so it's very important to understand that we have this lifecycle and 
the lifecycle are gonna be phases and the phases are gonna get bound to plug in goals. This is really the gist of 
how Maven is working. So the entire framework of Maven is designed to build or do these builds using plugins. A
build lifecycle with phases ties everything together for us. 

Out-of-the-box Maven have 3 predefined life cycles.
1. **Clean** - This does a clean of the project and really moves any build artifacts anything that we've done from our
working directory. It basically goes in cleans up everything and basically deletes anything that we've compiled 
or generated and usually it's gonna be dealing with by default the ***target directory***. It's gonna delete that and
anything in that. This is by default defined with plugin binding so that this out of the box Maven has plugin bindings. 

2. **Default** - This is what is going to do the build and deployment of your project. It is going to do the compiling, 
the testing, integration testing, and then the packaging, and deploying up to a Maven repo or any other deployment 
targets that we happen to define. In this case, that's a little bit different amongst the three. This does not have any 
plugin bindings by default. So the Default build lifecycle defines phases but the bindings are gonna be defined for 
each packaging type whether it's a JAR or WAR or EAR or POM, depending on the packaging type that we've defined for 
POM, that is going to drive the plugin bindings. 

3. **Site** - This actually creates a website for your project. This is, like the Clean life cycle, defined
with plugin bindings. This is probably the least used in enterprise. All Maven websites are generated with the site
plugin so it does a really great job of building a website for your project. 

### **A closer look at the Clean Lifecycle** 
Clean Lifecycle has 3 phases: 

* pre-clean
* clean
* post-clean

These are gonna run in order so pre-clean is gonna run, and then the clean is gonna run, and then post-clean. By
default there is no plugin bound to pre-clean or post-clean phases. However for clean, we have a plugin bound called 
the ***Maven Clean Plugin*** and the ***goal is clean***. So very important to remember that we have a lifecycle and
what's going to happen is Maven is going to run pre-clean. There's no plugin there. Nothing bound to any plugin goals. 
Now we have the clean phase and then it goes _**"ah I do have a plugin bound and we are gonna run the clean goal of that
plugin"**_. Next, post-clean. Again no plugins. 

### **A closer look at the Default Lifecycle** 
At a very high level these are the kind of top-level goals. 

* Validate
* Compile
* Test
* Package
* Verify
* Install
* Deploy

**Validate:** The Default lifecycle is going to go in and do a ***validate***. So the validate step goes in to make
sure that

* we have a project 
* our pom can be parsed 
* it has a proper XML 
* it matches the XML schema from Maven
* we actually have our standard directory structure. 

It's just gonna go through a series of checks and make sure you know kind of like a sanity check on our project. 

**Compile:** This is going to go through and for Java it would invoke the Java compiler and compile the source down
to bytecode for us. 

**Test:** Next, we test the compiled source code. It's going to run on any test that we have. 

**Package:** This is going to take the compiled files and move that to the target packaging type where there's a jar, 
ear or whatever. 

**Verify:** This is going to run the integration tests. 

**Install and Deploy:** This is going to install to our local maven repository or deploy to a shared maven repository 
or remote repository.

So this is a default lifecycle in a nutshell or at a very high level.

### **All the phases:** 

* Validate 
* Initialize 
* Generate Sources 
* Process Sources
* Generate Resources
* Process Resources
* Compile
* Process Classes

So these are very detailed things that we can hook into. A lot of times we don't have a need to tap into these. 
But as we get into more complex builds, we will need to tap into these. These are different hooks that we can put 
into our build process. So just continuing on here we have,

* Generate Test Sources
* Process Test Sources
* Generate Test Resources
* Process Test Resources
* Test Compile
* Prepare Test Classes
* Test 
* Prepare Package
* Package
* Pre-Integration Test
* Integration Test
* Post Integration Test 
* Verify
* Install
* Deploy 

So the default lifecycle is pretty complex. But out of the box, for just JAR packaging, we can see we have about
8 phases. 

### **Default Lifecycle - JAR Packaging**
* Phase: process-resources - Plugin: maven-resources-plugin: resources
* Phase: compile - Plugin: maven-compiler-plugin: compile
* Phase: process-test-resources - Plugin: maven-resources-plugin: testResources
* Phase: test-compile - Plugin: maven-compiler-plugin: testCompile
* Phase: test - Plugin: maven-surefire-plugin: test
* Phase: package - Plugin: maven-jar-plugin: jar
* Phase: install - Plugin: maven-install-plugin: install
* Phase: deploy - - Plugin: maven-deploy-plugin: deploy

### **A closer look at the Site Lifecycle**
This has 4 phases in it. 

1. pre-site - in this case there's no plugin associated. 
2. site - this is actually gonna be the plugin that's gonna go out and generate the site. This is going to go look 
at our project and generate all the HTML for it. 
3. post-site - There is no default plugin associated 
4. site-deploy - We can deploy the site. 

It's very important to understand in summary how these work together. We have the lifecycle, the phases, and the
phases then allow us to specify one or more plugin goals. The main takeaway is to understand that we do have 3
standard life cycles within Maven and those life cycles have multiple phases in it and those multiple phases can
be associated with goals from a variety of different Maven plugins to do work inside of our build.