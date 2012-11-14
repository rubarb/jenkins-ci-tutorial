Jenkins Configuration for a Python-based Project
=============

To demonstrate the Sauce plugin for Jenkins, let's create a new Jenkins Freestyle project for a Python project.

The test results will need to be in the [JUnit XML format]() in order for them to be displayed in Jenkins user interface and so that the Sauce plugin can parse the results.  There are several Python libraries which can produce the appropriate XML output, for this tutorial we are going to use [NoseXUnit](http://nosexunit.sourceforge.net/).

From the Jenkins dashboard page, click `New Job`

![New Job](##new-job.png?##)

Enter 'Sauce Java Demo' in the Job Name field and select `Build a free-style software project`.

![New Freestyle Project](##new-freestyle-project.png?##)

Our sample code is located in [github](https://github.com/rossrowe/sauce-ci-python-demo), so select `Git` in the `Source Code Management` section, enter `https://github.com/rossrowe/sauce-ci-python-demo` as the repository URL and enter `master` in the branch specifier.

![Git Setup](##git-setup.png?##)

Now let's add a build step which will run our tests.  Click on the `Add Build Step` menu in the `Build` section, and select `Execute Shell`

![Execute Shell](##execute-shell.png?##)

Enter `nosetests --with-nosexunit simple_test.py` in the `Command` field.

![Nose command](##nose-command.png?##)

Now let's enable the Sauce OnDemand support for a Jenkins Job can be enabled by checking the `Sauce OnDemand Support` checkbox.

![Sauce Configure](##sauce-configure.png##)

Select the `Enable Sauce Connect?` check box.  When selected, the Sauce plugin will launch an instance of [Sauce Connect](http://saucelabs.com/docs/sauce-connect) prior to the running of your Job.  This instance will be closed when the Job completes.

Click on the `WebDriver` radio button and select a browser to run our tests against (let's pick Firefox 15 running in Windows 2008)

![Sauce Configure](##sauce-configure.png##)

Further details on the environment variables set by the Sauce plugin can be found on the [Java sample project tutorial page](##04-Job-Configuration.md##)

To enable this, select the `Add post-build Action` within the `Post-build Actions` section. 

![Add Post-build action](##post-build-action.png##)

From the pop-up menu, select the `Publish JUnit test result report` option.

![JUnit Post-build action](##junit-post-build-action##)

Enter `target/NoseXUnit/core/*.xml` as the path to the test reports that are produced by your Jenkins Job, and check the `Embed Sauce OnDemand reports` checkbox.

![Embed Sauce Reports](##embed-nose-reports##)

That's it, our configuration is all setup, let's run the tests! 

* _Next_: [Integration with tests](##04-Integration-with-tests.md##)