Java Hello World Sample

This project contains a simple servlet application.

Running the application using the command-line

This project can be built with Apache Maven. 

Use the following steps to run the application locally:

    Execute full Maven build to create the target/JavaHelloWorldApp.war file:

    $ mvn clean install

    Download and install Apache Tomcat, then use it to run the built application from step 1:

	$ mvn tomcat7:deploy 
	$ mvn tomcat7:undeploy 
	$ mvn tomcat7:redeploy 
