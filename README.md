# Deployment_App
# Author: Thiago Pereira
Automated deploy - WebSphere

This application its only for use to Automated Deploys on WebSphere Application Server 8.x (or later);

First of all, its necessary to enable "Monitored Directory Deployment" option in Deployment Manager, to do this goes to: 

Applications > Global deployment Settings.

After that create the folder and subfolder monitoredDeployableApps/cluster in Dmgr root directory (e.g. /opt/IBM/WebSphere/AppServer/profiles/Dmgr) and
restart the Dmgr.

When Dmgr is started, check inside the directory monitoredDeployableApps and see if the following folders were created: 

servers;
deploymentProperties.

Now, you have 2 options for automated deploy:

#1 - If you have a clustered environment, create one folder for each cluster in monitoredDeployableApps/cluster directory or 
if you have a standalone environment create a folder inside monitoredDeployableApps/servers with you standalone JVM name;

With the first option, you only will upload the file into the directory (server or cluster) and WebSphere will do the deploy for you.

The only impediment for that is if application have any option like Class Mode (PARENT LAST), Resource Reference, the automated deploy will loose this settings. But has another trick for that - the option #2.

#2 - This option is my favorite one and for this I created the Deployment_App (Web UI to upload files), let me explain:

Firsly, WebSphere allows us to generate a report from the application and with that we can set the configuration for the automated deploy, but how?

- When you enabled the "Monitored Directory Deployment" the WebSphere created a deploymentProperties folder, and what is that? This folder do exactly the same thing that I told in #1 option, in other words, when you update the properties file inside the deploymentProperties folder the magic happens.


In wwwwwww you see a example of the file and its absolutely that.

--------------------------------------------------------------------------------------------------------------------------------

Now that you already knows about "Monitored Directory Deployment" I will explain how the Deployment_App works and how you can use in your environment:

Simple like fly, the application have a index.jsp with all application that I have in my environment (and its real) and each application have a link for another .jsp and this jsp use javazoom library (all the credits for the upload function - http://www.javazoom.net/jzservlets/uploadbean/uploadbean.html) for the upload fuction.

There are 5 fields or tags that you need to modified for your application works too and its:

- <% String directory = "directory for the EAR upload"; %>
- <% String tmpdirectory = "directory for the EAR upload/tmp"; %>
- <title>TITLE YOU WANT</title>
- <h2 style="text-align: center;">TITLE YOU WANT</h2>
- String str ="props file";

e.g.:

<% String directory = "/u/deploy/Hello_WorldEAR"; %>
<% String tmpdirectory = "/u/deploy/Hello_WorldEAR/tmp"; %>
<title>Hello_WorldEAR</title>
<h2 style="text-align: center;">DEPLOY AUTOMATIZADO - Hello_WorldEAR</h2>
String str ="/u/opt/IBM/WebSphere/AppServer/profiles/Dmgr01/monitoredDeployableApps/deploymentProperties/Hello_WorldEAR.props";

And what you need to do:

Import this project in your eclipse , do all the modifications and export the EAR and deploy in your WebSphere environment!


