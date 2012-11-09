Jenkins Job Configuration
=============

Freestyle/Maven projects
---

To configure the Sauce OnDemand settings for a Jenkins Job, select the `Configure` link on a Job 

![Job Configure](https://raw.github.com/saucelabs/jenkins-ci-tutorial/master/job-configure.png?login=saucelabs&token=de87203126c9a522d34c0cc90bb50dc3)

The Sauce OnDemand support for a Jenkins Job can be enabled by checking the `Sauce OnDemand Support` checkbox.

![Sauce Configure](https://raw.github.com/saucelabs/jenkins-ci-tutorial/master/sauce-configure.png?login=saucelabs&token=de87203126c9a522d34c0cc90bb50dc3)

By selecting the `Enable Sauce Connect?` check box, the Sauce plugin will launch an instance of [Sauce Connect](http://saucelabs.com/docs/sauce-connect) prior to the running of your Job.  This instance will be closed when the Job completes.

Sauce OnDemand supports a wide range of browsers, but some browser combinations are only supported for SeleniumRC or WebDriver tests.  The multi-select lists beneath the `SeleniumRC` and `WebDriver` radio buttons are populated by retrieving the list of respective supported browsers via the Sauce REST API.

If a single browser is selected, then the `SELENIUM_PLATFORM`, `SELENIUM_VERSION`, `SELENIUM_BROWSER` and `SELENIUM_DRIVER` environment variables will be populated to contain the details of the selected browser.  If multiple browsers are selected, then the `SELENIUM_BROWSER` environment variable will be populated with a JSON-formatted string containing the attributes of the selected browsers.  An example of the JSON string is:

```json

[{
	"platform":"LINUX",
	"os":"Linux",
	"browser":"firefox",
	"url":"sauce-ondemand:?os=Linux&browser=firefox&browser-version=16","browser-version":"16"},
{
	"platform":"VISTA",
	"os":"Windows 2008",
	"browser":"iexploreproxy",
	"url":"sauce-ondemand:?os=Windows 2008&browser=iexploreproxy&browser-version=9",
	"browser-version":"9"}]
```

If the `SeleniumRC` radio button is selected, then a `Starting URL` field will also be displayed.

The plugin will set a series of environment variables based on the information provided on the Job Configuration. These environment variables can either be explicitly referenced by your unit tests, or through the use of the [selenium-client-factory] library.

* SELENIUM_HOST - The hostname of the Selenium server
* SELENIUM_PORT - The port of the Selenium server
* SELENIUM_PLATFORM - The operating system of the selected browser
* SELENIUM_VERSION - The version number of the selected browser
* SELENIUM_BROWSER - The browser name of the selected browser.
* SELENIUM_DRIVER - Contains the operating system, version and browser name of the selected browser, in a format designed for use by the [Selenium Client Factory]()
* SAUCE_ONDEMAND_BROWSERS - A JSON-formatted string representing the selected browsers
* SELENIUM_URL - The initial URL to load when the test begins
* SAUCE_USER_NAME - The user name used to invoke Sauce OnDemand
* SAUCE_API_KEY - The access key for the user used to invoke Sauce OnDemand
* SELENIUM_STARTING_URL - The value of the `Starting URL` field

By default, the plugin will use the authentication details specified in the Jenkins administration section.  However, this can be overriden at the Job level by enabling the `Override default authentication?` checkbox and specifying values in the `Username` and `Access key` fields.

Note: These values are set automatically by the Jenkins plugin. If the `Enable Sauce Connect?` checkbox is selected, then the `SELENIUM_HOST` and `SELENIUM_PORT` variables will default to localhost:4445.  If the checkbox is not set, then the `SELENIUM_HOST` and `SELENIUM_PORT` variables will be set to ondemand.saucelabs.com:4444.  

The values for the `SELENIUM_HOST` and `SELENIUM_PORT` environment variables can be overridden by explicitly specifying the host and port in the `Sauce OnDemand Host` and `Sauce OnDemand Port` fields, which can be displayed by clicking on the `Sauce Connect Advanced Options` button.

![Sauce Configure](https://raw.github.com/saucelabs/jenkins-ci-tutorial/master/sauce-configure.png?login=saucelabs&token=de87203126c9a522d34c0cc90bb50dc3)

Multi-configuration projects
---

* _Next_: [Integration with tests](https://github.com/saucelabs/java-tutorial/blob/master/04-Integration-with-tests.md)
