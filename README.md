# openmrs-distro-oclqa


<img src="https://cloud.githubusercontent.com/assets/668093/12567089/0ac42774-c372-11e5-97eb-00baf0fccc37.jpg" alt="OpenMRS"/>

QA Environment for the OCL Subscription Module

OCL Subscription Module (Design Page)

Development environment
Please make sure you have the following installed:

MySQL 5.6.x
JDK 1.7
Maven
OpenMRS SDK, see installation instructions
Next run this command to setup OpenMRS server (just the first time):

$ mvn openmrs-sdk:setup -DserverId=refapp -Ddistro=referenceapplication:2.11
# Note: Pick default values for everything except MySQL username and password
If there are any issues with setting up the server, check out OpenMRS SDK documentation

Deploy OWA module on the server:

$ mvn openmrs-sdk:deploy -DserverId=refapp -DartifactId=owa -Dversion=1.6.3
You also need to deploy webservices.rest module:

$ mvn openmrs-sdk:deploy -DartifactId=webservices.rest -Dversion=2.17-SNAPSHOT -DserverId=refapp
Fork and clone Open Concept Lab module project:

$ mvn openmrs-sdk:clone -DartifactId=openconceptlab
$ cd openmrs-module-openconceptlab
Build and install the module on the server:

$ mvn clean install openmrs-sdk:deploy -DserverId=refapp
You can also configure the server to automatically reload classes and pages from the omod directory:

$ mvn openmrs-sdk:watch -DserverId=refapp
Run the server:

$ mvn openmrs-sdk:run -DserverId=refapp
Once you run the command you need to wait for Jetty Started message, open up a browser ang go to:

http://localhost:8080/openmrs

The server can be stopped from the terminal, in which it is running with the Ctrl and C (Ctrl + C) keys combination.

Every time you make changes in code in the api directory, you need to build and install the module and restart the server.

Alternatively you can upload *.omod file via Advanced Administration -> Manage Modules panel. This way you will not have to restart the server.

OCL Module is now available from the Advanced System Administration or at /openmrs/openconceptlab/status.page

### Running Cypress Tests
As opposed to the tests built into the package using Jest, we also supply some end-to-end tests written using [Cypress](https://www.cypress.io/). These are run automatically on each PR or commit. In the CI environments, we actually spin up a local instance of the OCL API and then the OpenMRS Dictionary Manager via Docker. This can be done locally by running the [`start_local_instance.sh`](start_local_instance.sh) script. From there, the CI will run `npm test:integration` which will run Cypress and all tests locally.

If Cypress fails to run on your local instance for whatever reason, you can use the [`run_e2e.sh`](run_e2e.sh) script to run the Cypress tests inside a Docker container. This is useful for running the tests locally, but if tests fail, it is easier to use the Cypress UI to diagnose the issues. To run Cypress with the UI (assuming Cypress works locally), you can run `npx cypress open`. Unfortunately, it's not possible to run the Cypress UI in the Docker container to the best of my knowledge.

## Contributing to this project


### Gotchas
Things we've pulled our hair out for so you don't have to
- Have an env-config file before running the e2e tests

## Support
- Talk to us at [OpenMRS Talk](https://talk.openmrs.org/)

## License
- [MPL 2.0 w/ HD](http://openmrs.org/license/) © [OpenMRS Inc.](http://www.openmrs.org/)
