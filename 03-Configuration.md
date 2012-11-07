Configuring the Jenkins Sauce OnDemand plugin
=============

After the Sauce plugin has been installed, the username and access key of the Sauce OnDemand user account must be entered.

To configure the authentication, first click `Manage Jenkins` from the left-hand navigation pane.

![Manage Jenkins](https://raw.github.com/saucelabs/jenkins-ci-tutorial/master/manage-jenkins.png?login=saucelabs&token=de87203126c9a522d34c0cc90bb50dc3)

Click the `Configure System` link

![Configure System](https://raw.github.com/saucelabs/jenkins-ci-tutorial/master/configure-system.png?login=saucelabs&token=de87203126c9a522d34c0cc90bb50dc3)

Scroll down to the `Sauce OnDemand` section.

![Sauce Admin](https://raw.github.com/saucelabs/jenkins-ci-tutorial/master/sauce-admin.png?login=saucelabs&token=de87203126c9a522d34c0cc90bb50dc3)

This section contains the fields required to configure how the authentication for the Sauce plugin.  Enter the values of the username and access key you wish the Sauce plugin to use in the `Username` and `API Access Key fields`.  

By default, the Sauce plugin will use the user home directory as the working directory when extracting the Sauce Connect Jar file.  You can override this behaviour by specifying a directory location in the `Sauce Connect Working Directory` field.

The plugin also supports reading authentication details from a `.sauce-ondemand` file located in the user home directory.  If you wish the plugin to use this file, then select the `Use authentication details in ~/.sauce-ondemand?` checkbox.

Once the authentication details have been entered, clicking on the `Test Connection` button will connect to Sauce OnDemand to verify that the plugin can authenticate with the entered details.

The plugin includes a copy of the Sauce Connect Jar file.  When the administration screen is displayed, the plugin will check to see if a later version of Sauce Connect is available, and if so, will provide a link that will download the updated version without requiring a new version of the Sauce plugin to be installed.

Once the authentication details have been entered and saved on the `Configure System` screen, you can then enable Sauce OnDemand support on the Configuration screen for a Jenkins Job.


Freestyle/Maven projects

To configure the Sauce OnDemand settings for a Jenkins Job, select the `Configure` link on a Job 

![Job Configure](https://raw.github.com/saucelabs/jenkins-ci-tutorial/master/job-configure.png?login=saucelabs&token=de87203126c9a522d34c0cc90bb50dc3)

The Sauce OnDemand support for a Job can be enabled by checking the `Sauce OnDemand Support` checkbox.

![Sauce Configure](https://raw.github.com/saucelabs/jenkins-ci-tutorial/master/sauce-configure.png?login=saucelabs&token=de87203126c9a522d34c0cc90bb50dc3)

By selecting the `Enable Sauce Connect?` check box, the Sauce plugin will launch an instance of [Sauce Connect](http://saucelabs.com/docs/sauce-connect) prior to the running of your Job.  This instance will be closed when the Job completes.

Sauce OnDemand supports a wide range of browsers, but some browser combinations are only supported for SeleniumRC or WebDriver tests.  The multi-select lists beneath the `SeleniumRC` and `WebDriver` radio buttons are populated by retrieving the list of respective supported browsers via the Sauce REST API.

If the `SeleniumRC` radio button is selected, then a `Starting URL` field will be displayed.

The plugin will set a series of environment variables based on the information provided on the Job Configuration. These environment variables can either be explicitly referenced by your unit tests, or through the use of the [selenium-client-factory] library.

* SELENIUM_HOST - The hostname of the Selenium server
* SELENIUM_PORT - The port of the Selenium server
* SELENIUM_PLATFORM - The operating system of the selected browser
* SELENIUM_VERSION - The version number of the selected browser
* SELENIUM_BROWSER - The browser string.
* SELENIUM_URL - The initial URL to load when the test begins
* SAUCE_USER_NAME - The user name used to invoke Sauce OnDemand
* SAUCE_API_KEY - The access key for the user used to invoke Sauce OnDemand

Note: These values are set automatically by the Jenkins plugin. If you are using Sauce Connect, SELENIUM_HOST and SELENIUM_PORT are set to ondemand.saucelabs.com:4445, such that all communication with our browsers is encrypted.

Multi-configuration projects

* _Next_: [ Sauce Jenkins plugin](https://github.com/saucelabs/java-tutorial/blob/master/03-Configuration.md)