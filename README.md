Sample complete test automation framework for UI and API end 2 end testing
This sample Software Test Automation Framework is built as a Maven project using Behavior Driven Development principles with Cucumber and Junit in Java. and also utilized Page Object Module structure to maximize framework reusability and maitainability.  And the scenario is written in Gherkin language which is a plain English, that could benefit connecting the team.

And framework is also structured to support API testing using RestAssured with Database integration capabilities with JDBC.
Project structure:
src/test/java

api_tests - (API tests written using RestAssured library in TestNG structure).
pages - (Page objects are created)
runners - (one or more cucumber runner classes are created )
step_definitions - (test steps implementations for scenario steps define in the feature file)
utilities - (methods and support classes are created) 
src/test/resources
features - (cucumber feature files for define scenarios for the feature)
testdata - (Test data/ properties files are stored)
testfiles - (Test json or any dummy files are stored)
pom.xml - (Project configuration, content/library/dependencies manage and build/run configuration) 
testng.xml - (TestNg test suite managment and execution control)

## Tools used for UI test automation

-Maven -(Project configuration, content/library/dependencies manage and build/run configuration)

-Cucumber - (define feature scenarios in Gherkin, also control test flow, create test suite and execution flow with tagging and reporting)

-Selenium -(used for automate the Web Application by implementing the step definitiion, managing the page object)

-WebDriver Manager -(used to manage the browser driver binary  auto downloading the setting browser driver)

-Junit - (Used to run the cucumber scenarios with cucumber options)

-JDBC - (connet to the database for testing activities)

- MySQL driver - (allow connection to mysql database that application uses)

## automation tools for API

-TestNg - (manage the api test suite, test execution flow and assertion, reporting)

- RestAssured (define API tests)

-JDBC - (connet to the database for testing activities)

- MySQL driver - (allow connection to mysql database that application uses)

Shared tools used for end to end testing

-Git - (Source code management/ version control)

-GitHub - (remode source code managment/ version control platform)

-Jenkins -(CI/CD tool which we have use to run test suites)

-Eclipse -(IDE for project development)




Creating UI tests: [Cucumber docs](file:///Users/sheralie/eclipse-workspace/cucumberProjectFinal/test_results/cucumber_report.html)

1. create a feature file under src/test/resource folder with extention.feature
2.defind scenario with cucumber key words like Given When Then And structure
3.Generate step definition snippeds (dry run)
4. Create a steps class under 'step_definition' folder and put those generated steps snippets
5.Create page classes under 'pages' folder and define the page objects (elements)
6.Implemet the step definitions based on scenario behaviours

Running the UI tests

1. Create a runner class under 'runner' folder
2.defind the RunWith cucumber options with necessary options
3. Pass a scenario tag to execute tests using cucumber tags
4.To run the tests remotely via a CI/CD tools like Jenkins, create a build in pom.xml
and point to the runner class in build configuration. (refer to existing pom.xml for examples)
5. On Jenkins job under build flow, select top leve; maven target and pass the foloowing commad:
```
clean test -Dcucumber.filter.tags="@smoketest"
```
 
Creating API tests:[RestAssured docs](https://Rest-assured.io/)

1. create a class in 'api_tests' folder under 'src/test/java' folder
2.Create a TestNG test and define the API test flow with RestAssured


Running the test

1.run the particular API test class as a TestNG test
2. to run the API test remotely via CI/CD too like Jenkins, create a TestNG xml file
and define a TestNG suite that includes certain API test classes to execute.
3.Create a profile in pom.xml that includes the TestNG xml as a test suite.
4. On Jenkins job under build workflow, select top leve; maven target and pass the foloowing commad:
```
clean test -P<profileId>
```

Profile example:
<profiles>
		<profile>
			<id>api_tests</id>
			<build>
				<plugins>
					<plugin>
						<groupId>org.apache.maven.plugins</groupId>
						<artifactId>maven-surefire-plugin</artifactId>
						<version>3.0.0-M5</version>
						<configuration>
							<suiteXmlFiles>
								<suiteXmlFile>testng.xml</suiteXmlFile>
							</suiteXmlFiles>
						</configuration>
					</plugin>
				</plugins>
			</build>
		</profile>
	</profiles>

