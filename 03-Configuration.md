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

* _Next_: [Jenkins Job Configuration](https://github.com/saucelabs/java-tutorial/blob/master/04-Job-Configuration.md)