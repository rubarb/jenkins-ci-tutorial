Multi-configuration projects
---

Jenkins [Multi-configuration projects](https://wiki.jenkins-ci.org/display/JENKINS/Building+a+matrix+project) allow you to run the same build with different input parameters.  The Sauce plugin for Jenkins provides an additional option for multi-configuration projects to specify the browser combination for each build.

To configure this on a multi-configuration job, click on the `Add Axis` button and select either the `Sauce OnDemand WebDriver tests` or `Sauce OnDemand SeleniumRC tests' item.  

![Sauce Configure](##multi-config-matrix.png##)

This will present a list of browser combinations that are supported by Sauce Labs for WebDriver and SeleniumRC.

![WebDriver browsers](##sauce-matrix-webdriver.png##)

For each selected browsers, a separate job will run when the build is invoked.  This job will include `SELENIUM_PLATFORM`, `SELENIUM_VERSION`, `SELENIUM_BROWER`, and `SELENIUM_DRIVER` system properties which will be set to the corresponding browser.