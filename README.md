# mule4-deployment-demo
PoC for deploying MuleSoft applications via Mule Maven Plugin.
###### This is repo is currently a work in progress

## What is a Mule Maven Plugin?
* allows you to deploy/undeploy a MuleSoft application. It works with the Enterprise Mule Runtime engine and Community Mule Kernel.
* capable of deploying applications automatically to on-premise, CloudHub, and Anypoint Runtime Fabric Manager.

## 3 Goals of the Mule Maven plugin supports:
* Package: Generates jar or executable files for your Mule application.
```
o	mvn package
```
* Deploy: It automatically uploads, deploys and starts the application on the target system (on-premise, CloudHub, Anypoint Runtime Fabric).
```
o	mvn deploy -DmuleDeploy
```
* Undeploy: It automatically removes the application from the target system (on-premise, CloudHub, Anypoint Runtime Fabric).
```
o	mvn mule:undeploy
```
The Mule Maven Plugin is found in the POM.xml. It is created by default whenever you create a Mule application, otherwise, you can define the plugin in POM.xml as shown below:

### XML
```
<p>
<groupId>org.mule.tools.maven</groupId>
<artifactId>mule-maven-plugin</artifactId>
<version>3.3.5</version>
</plugin>
```

### Mule Maven Plugin is capablie of deploying applications to Anypoint CloudHub. 
The following are Mule Maven Plugin parameters required for deploying applications to CloudHub:

|Parameter Description|    |       
| ------------- |:-------------:| 
|uri | Your Anypoint Platform URI. If not set, by default this value is set to https://anypoint.mulesoft.com | 
|muleVersion | The Mule runtime engine version that will run in your CloudHub instance.|   
|username | Your Cloudhub username.|
|password | Your Cloudhub password.|  
|applicationName | The name of your application in CloudHub.|
|server | Maven server with Anypoint Platform credentials.|
|workers | The number of workers. By default, it is set to 1.| 
|workerType | Size of each worker. The default value is MICRO.| 
|environment | The CloudHub environment to which you want to deploy.|
|businessGroup | The name of your business group.|
|region | Region of workers cloud. The default value is us-east-1.|
|properties | if you need to set properties for the Mule application you are deploying, you can use the <properties> top-level element:|

properties example:
```
<properties>
<key>value</key>
</properties>
For example:
<properties>
<http.url>http://abc.com/employees</http.url>
</properties>
```

### Worker Size
*	MICRO (default; 0.1 vCores)
*	SMALL (0.2 vCores)
*	MEDIUM (1 vCore )
*	LARGE (2 vCores)
*	XLARGE (4 vCores)
*	XXLARGE (8 vCores)
*	4XLARGE (16 vCores)

### Worker Region
*	us-east-1 (default; US East, N. Virginia)
*	us-east-2 (US East, Ohio)
*	us-west-1 (US West, N. California)
*	us-west-2 (US West, Oregon)
*	eu-central-1 (EU, Frankfurt)
*	eu-west-1 (EU, Ireland)
*	eu-west-2 (EU, London)
*	ap-southeast-1 (Asia Pacific, Singapore)
*	ap-southeast-2 (Asia Pacific, Sydney)
*	ap-northeast-1 (Asia Pacific, Tokyo)
*	ca-central-1 (Canada, Central)
*	sa-east-1 (South America, São Paulo)

For deploying applications to CloudHub using Mule Maven Plugin, you need a configuration in POM.xml as shown below:

### XML

```
   <groupId>org.mule.tools.maven</groupId>
   <artifactId>mule-maven-plugin</artifactId>
   <version>3.3.5</version>
   <extensions>true</extensions>
   <configuration>
      <cloudHubDeployment>
         <username>Anypoint Username</username>
         <p>Anypoint Password</password>         
         <workers>1</workers>
         <workerType>Micro</workerType>
         <environment>Sandbox</environment>
         <muleVersion>4.2.2</muleVersion>
         <applicationName>Mule4-Linabel-Demo</applicationName>
      </cloudHubDeployment>
   </configuration>
</plugin>
```
To deploy applications to CloudHub, you need to execute the below command:
```
 mvn package deploy -DmuleDeploy
 ```
 
Currently, in the above configuration, we have hard coded all the values for the parameter. Instead of passing hard coded values, we can define properties for each parameter and pass properties values through a maven command as shown below:     

### XML
```
<plugin>
   <groupId>org.mule.tools.maven</groupId>
   <artifactId>mule-maven-plugin</artifactId>
   <version>3.3.5</version>
   <extensions>true</extensions>
   <configuration>
      <cloudHubDeployment>
         <username>${username}</username>
         <p>${password}</password>         
         <workers>${workers}</workers>
         <workerType>${worker.type}</workerType>
         <environment>${environment}</environment>
         <muleVersion>${mule.version}</muleVersion>
         <applicationName>${application.name}</applicationName>
      </cloudHubDeployment>
   </configuration>
</plugin>
```

To deploy an application to CloudHub, you need to execute the below command:
```
 mvn package deploy -DmuleDeploy -Dusername=AnypointUsername -Dpassword=AnypointPassword -Dworkers=1 -Dworker.type=Micro -Denvironment=Sandbox -Dmule.version=4.2.2
```

You can see some issues that we are passing password in cleartext, and it is not recommended to store your password in cleartext. Please click on this link; it will explain how to encrypt your Anypoint Platform password in POM with Maven to deploy an application into CloudHub.


### Mule Maven Plugin has the capability of deploying applications to on-premise MuleSoft runtime. 
The following are Mule Maven Plugin parameters required for deploying applications to MuleSoft runtime.

|Parameter Description|    |       
| ------------- |:-------------:| 
|muleVersion | The Mule version running in your local machine instance|   
|muleHome | The location of the Mule instance in your local machine.|


For deploying applications to on-premises, you need to do below configuration in POM.xml.
```
<p>
   <groupId>org.mule.tools.maven</groupId>
   <artifactId>mule-maven-plugin</artifactId>
   <version>3.3.5</version>
   <extensions>true</extensions>
   <configuration>
      <standaloneDeployment>
         <muleVersion>${mule.version}</muleVersion>
         <muleHome>${mule.home}</muleHome>        
      </standaloneDeployment>
   </configuration>
</plugin>
```

To deploy Application to on-premise, you need to execute the below command:
```
 mvn package deploy -DmuleDeploy -Dmule.version=4.2.2 -Dmule.home=/mule/bin  
```

### Tutorials:
#### [Deploy Mulesoft Application to Cloudhub Using Mule Maven Plugin](https://github.com/Linabel-Tech/mule4-demo/tree/master/deploy-app-cloudhub)
#### Deploy Mulesoft Application to CloudHub using Jenkins and Maven
#### Encrypt Anypoint Platform password in POM with Maven
#### Configuring Jenkins CI/CD Pipeline For Mulesoft Applications
#### Create Postman Test Collection Suite for Mulesoft API
#### Performance or Load Testing for Mulesoft API Using Apache JMeter

