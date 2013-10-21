---
layout: post
title:  "Automated Web Deployment with MSBuild and MSDeploy"
date:   2011-10-13 16:17:00
categories: Work DotNet
---

If you are looking for an automated web deployment process you will inevitably come to MSBuild.
There are many tutorials out [there][1] how to set up a command line call for MSBuild but you wont find a documentation how to publish a generated package with MSDeploy.

But this is especially needed is you want to use “-setParam” for a tokenized (transformed) web.config file and wont / can't change the SetParameter.xml!
(The names of the parameters for -setParam can be found in the SetParameter.xml file in the same directory as the Package.zip. They are also act as default values if not set in the command line call. )

So I wrote this quick tutorial how to get command line call for MSDeploy.
(Please consider that the paths you will later use are absolute / relative to the working directory.)

**Step 1: Get the publish ready with MSBuild**

Before we will get some further results please get your deployment call working.

```
msbuild.exe
SomeWebProject.csproj
/P:Configuration=Release
/P:DeployOnBuild=True
/P:DeployTarget=MSDeployPublish
/P:MsDeployServiceUrl=https://TargetServer/MsDeploy.axd
/P:AllowUntrustedCertificate=True
/P:MSDeployPublishMethod=WMSvc
/P:CreatePackageOnPublish=True
/P:UserName=Username
/P:Password=Password
/P:DeployIisAppPath=TargetWebSite/TargetWebApp
```

* Configuration: This is the configuration you will use eg. Debug, Release or a custom one
* AllowUntrustedCertificate: You will need this if you do not have a valid certificate on the server
* DeployIisAppPath: The name of the target website eg. “Default Web Site/MyWebApp”
* TargetWebSite/TargetWebApp: Please consider the different usages below!

**Step 2: Get the command line for MSDeploy**

Append the parameter `/P:UseMsdeployExe=True` to the `msbuild.exe` call. If you do so, you will see the call in the console like this:

```
MSDeployPublish:
Start Web Deploy Publish the Application/package to https:/TargetServer/MsDeploy.axd?site=TargetWebSite...
Running msdeploy.exe.
msdeploy.exe -source:package='C:\SomeWebProject\obj\Release\Package\SomeWebProject.zip' -dest:auto,ComputerName='https://TargetServer:8172/MsDeploy.axd?site=TargetWebSite',UserName='Username',Password='Password',IncludeAcls='False',AuthType='Basic' -verb:sync -disableLink:AppPoolExtension -disableLink:ContentExtension -disableLink:CertificateExtension -allowUntrusted -retryAttempts=2
```

Gotcha! This is the important MSDeploy command line call.

**Step 3: Get the two things together**

now we can split the automatic deployment of MSBuild into 1. create only the package with MSBuild and 2. only deploy with MSDeploy.

```
msbuild.exe
SomeWebProject.csproj
/P:Configuration=Release
/P:DeployOnBuild=True
/P:CreatePackageOnPublish=True

msdeploy.exe
-source:package='C:\SomeWebProject\obj\Release\Package\SomeWebProject.zip'
-dest:auto,ComputerName='https://TargetServer:8172/MsDeploy.axd?site=TargetWebSite',UserName='Username',Password='Password',IncludeAcls='False',AuthType='Basic'
-verb:sync
-disableLink:AppPoolExtension
-disableLink:ContentExtension
-disableLink:CertificateExtension
-allowUntrusted
-retryAttempts=2
-setParam:'IIS Web Application Name'='TargetWebSite/TargetWebApp'
```

**_Have a nice day._**

   [1]: http://www.troyhunt.com/2010/11/you-deploying-it-wrong-teamcity_11.html