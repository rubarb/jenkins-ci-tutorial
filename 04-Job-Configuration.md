Jenkins Configuration for a Java-based Project
=============

To demonstrate the Sauce plugin for Jenkins, let's create a new Jenkins Freestyle project for a Java project.

From the Jenkins dashboard page, click `New Job`

![New Job](##new-job.png##)

Enter 'Sauce Java Demo' in the Job Name field and select `Build a free-style software project`.

![New Freestyle Project](##new-freestyle-project.png##)

Our sample code is located in [github](https://github.com/rossrowe/sauce-ci-java-demo), so select `Git` in the `Source Code Management` section, enter `https://github.com/rossrowe/sauce-ci-java-demo` as the repository URL and enter `master` in the branch specifier.

![Git Setup](##git-setup.png##)

Now let's add a build step which will run our tests.  Click on the `Add Build Step` menu in the `Build` section, and select `Invoke top-level Maven targets`

![Invoke Maven](##invoke-maven.png##)

Enter `test` in the `Goals` field.

![Maven Goals](##maven-goal.png##)

Now let's enable the Sauce OnDemand support for a Jenkins Job can be enabled by checking the `Sauce OnDemand Support` checkbox.

![Sauce Configure](##sauce-configure.png##)

Select the `Enable Sauce Connect?` check box.  When selected, the Sauce plugin will launch an instance of [Sauce Connect](http://saucelabs.com/docs/sauce-connect) prior to the running of your Job.  This instance will be closed when the Job completes.

Click on the `WebDriver` radio button and select a browser to run our tests against (let's pick Firefox 15 running in Windows 2008)

![Sauce Configure](##sauce-configure.png##)

Sauce OnDemand supports a wide range of browsers, but some browser combinations are only supported for SeleniumRC or WebDriver tests.  The multi-select lists beneath the `SeleniumRC` and `WebDriver` radio buttons are populated by retrieving the list of respective supported browsers via the Sauce REST API.

If a single browser is selected, then the `SELENIUM_PLATFORM`, `SELENIUM_VERSION`, `SELENIUM_BROWSER` and `SELENIUM_DRIVER` environment variables will be populated to contain the details of the selected browser.  If multiple browsers are selected, then the `SELENIUM_BROWSER` environment variable will be populated with a JSON-formatted string containing the attributes of the selected browsers.  An example of the JSON string is:

```json

[
	{
	"platform":"LINUX",
	"os":"Linux",
	"browser":"firefox",
	"url":"sauce-ondemand:?os=Linux&browser=firefox&browser-version=16",
	"browser-version":"16"
	},
	{
	"platform":"VISTA",
	"os":"Windows 2008",
	"browser":"iexploreproxy",
	"url":"sauce-ondemand:?os=Windows 2008&browser=iexploreproxy&browser-version=9",
	"browser-version":"9"
	}
]
```

If the `SeleniumRC` radio button is selected, then a `Starting URL` field will also be displayed.

The plugin will set a series of environment variables based on the information provided on the Job Configuration. These environment variables can either be explicitly referenced by your unit tests, or through the use of the [selenium-client-factory] library.

* `SELENIUM_HOST` - The hostname of the Selenium server
* `SELENIUM_PORT` - The port of the Selenium server
* `SELENIUM_PLATFORM` - The operating system of the selected browser
* `SELENIUM_VERSION` - The version number of the selected browser
* `SELENIUM_BROWSER` - The browser name of the selected browser.
* `SELENIUM_DRIVER` - Contains the operating system, version and browser name of the selected browser, in a format designed for use by the [Selenium Client Factory]()
* `SAUCE_ONDEMAND_BROWSERS` - A JSON-formatted string representing the selected browsers
* `SELENIUM_URL` - The initial URL to load when the test begins
* `SAUCE_USER_NAME` - The user name used to invoke Sauce OnDemand
* `SAUCE_API_KEY` - The access key for the user used to invoke Sauce OnDemand
* `SELENIUM_STARTING_URL` - The value of the `Starting URL` field

By default, the plugin will use the authentication details specified in the Jenkins administration section.  However, this can be overriden at the Job level by enabling the `Override default authentication?` checkbox and specifying values in the `Username` and `Access key` fields.

Note: These values are set automatically by the Jenkins plugin. If the `Enable Sauce Connect?` checkbox is selected, then the `SELENIUM_HOST` and `SELENIUM_PORT` variables will default to localhost:4445.  If the checkbox is not set, then the `SELENIUM_HOST` and `SELENIUM_PORT` variables will be set to ondemand.saucelabs.com:4444.  

The values for the `SELENIUM_HOST` and `SELENIUM_PORT` environment variables can be overridden by explicitly specifying the host and port in the `Sauce OnDemand Host` and `Sauce OnDemand Port` fields, which can be displayed by clicking on the `Sauce Connect Advanced Options` button.

![Sauce Configure](##sauce-configure.png##)

Embedding Sauce Reports
---

The plugin also supports the embedding of Sauce Job reports within the display of test results.  This requires the tests executed by the Jenkins job to produce result files in the [JUnit XML]() report format. 

To enable this, select the `Add post-build Action` within the `Post-build Actions` section. 

![Add Post-build action](##post-build-action.png##)

From the pop-up menu, select the `Publish JUnit test result report` option.

![JUnit Post-build action](##junit-post-build-action##)

Enter `target/surefire-reports/*.xml` as the path to the test reports that are produced by your Jenkins Job, and check the `Embed Sauce OnDemand reports` checkbox.

![Embed Sauce Reports](##embed-sauce-reports##)

That's it, our configuration is all setup, let's run the tests!

* _Next_: [Integration with tests](##04-Integration-with-tests.md##)
