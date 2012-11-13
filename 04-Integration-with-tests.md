Integrating tests with the Jenkins Sauce OnDemand plugin
=============

In order to make the most use out of the Sauce Jenkins plugin, the following steps should be performed:

* Update tests to reference the environment variables set by the plugin
* Output the Sauce session id to the stdout to allow the Sauce plugin to associate test results to Sauce Jobs 

Referencing Job Configuration
---

As mentioned previously, the Sauce Jenkins plugin will set a series of environment variables that reflect the values entered on the Jenkins Job Configuration screen.

Your test code will need to be updated to reference these environment variables.  

Below is some sample Java code which demonstrates how to reference the environment variables that are set by the Jenkins plugin

<!-- SAUCE:LOGIN -->
```java
	DesiredCapabilities desiredCapabilities = new DesiredCapabilities();
	desiredCapabilities.setBrowserName(System.getenv("SELENIUM_BROWSER"));
	desiredCapabilities.setVersion(System.getenv("SELENIUM_VERSION"));
	desiredCapabilities.setCapability(CapabilityType.PLATFORM, System.getenv("SELENIUM_PLATFORM"));
	WebDriver driver = new RemoteWebDriver(
				new URL("http://<!-- SAUCE:USERNAME -->:<!-- SAUCE:ACCESS_KEY -->@ondemand.saucelabs.com:80/wd/hub"),
                desiredCapabilities);

```

Output Sauce Session id
---

As part of the post build activities, the Sauce plugin will parse the test result files. It attempts to identify lines in the stdout or stderr that are in the following format:

	SauceOnDemandSessionID=<some session id> job-name=<some job name>
	
The session id can be obtained from the `RemoteWebDriver` instance and the job-name can be any string, but is generally the name of the test class being executed.

Below is a Java sample that demonstrates outputting the session id to the Java stdout.

```java
private void printSessionId() {
		
        String message = String.format("SauceOnDemandSessionID=%1$s job-name=%2$s", (((RemoveWebDriver) driver).getSessionId()).toString(), "some job name");
        System.out.println(message);
    }
