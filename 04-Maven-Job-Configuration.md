Jenkins Configuration for a Java-based Project
=============

The setup for Maven projects is essentially the same as for Freestyle projects, but there's a couple of extra steps.  Let's create a new Jenkins Maven project for our Java demo project.

From the Jenkins dashboard page, click `New Job`

![New Job](##new-job.png##)

Enter 'Sauce Java Maven Demo' in the Job Name field and select `Build a maven 2/3 project`.

![New Freestyle Project](##new-maven-project.png##)

Our sample code is located in [github](https://github.com/rossrowe/sauce-ci-java-demo), so select `Git` in the `Source Code Management` section, enter `https://github.com/rossrowe/sauce-ci-java-demo` as the repository URL and enter `master` in the branch specifier.

![Git Setup](##git-setup.png##)

Enter `test` in the `Goals and options` field.

![Maven Goals](##maven-goal-option.png##)

Now let's enable the Sauce OnDemand support for a Jenkins Job can be enabled by checking the `Sauce OnDemand Support` checkbox.

![Sauce Configure](##sauce-configure.png##)

Select the `Enable Sauce Connect?` check box.  When selected, the Sauce plugin will launch an instance of [Sauce Connect](http://saucelabs.com/docs/sauce-connect) prior to the running of your Job.  This instance will be closed when the Job completes.

Click on the `WebDriver` radio button and select a browser to run our tests against (let's pick Firefox 15 running in Windows 2008)

![Sauce Configure](##sauce-configure.png##)

To enable the embedding of Sauce OnDemand reports for test results, select the `Add post-build Action` within the `Post-build Actions` section, and select the `Additional test report feature (Sauce OnDemand)` option.

Select the `Add post-build Action` action again, and select the `Additional test report feature` option, and check the `Embed Sauce OnDemand reports` checkbox.

![Maven Post-build action](##maven-post-build.png##)

That's it, our configuration is all setup, let's run the tests!

* _Next_: [Integration with tests](##04-Integration-with-tests.md##)
