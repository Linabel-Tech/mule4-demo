### Prerequisite

- [ ] Open [Mulesoft Cloudhub account] (https://anypoint.mulesoft.com/login/signup)

- [ ] Download [Maven] (http://maven.apache.org/download.cgi?Preferred=ftp://ftp.osuosl.org/pub/apache/)

- [ ] Install [Maven using a Mac] (https://github.com/Linabel-Tech/mule4-demo/blob/master/deploy-app-cloudhub/install-mvn-mac.md)

- [ ] Download [Anypoint Studio] (https://www.mulesoft.com/platform/studio)


### Deploy Mulesoft Application to Cloudhub Using Mule Maven Plugin

**Step 1:** Create Mule Project: **File -> New -> Mule Project**. Give your project a name. Make sure Runtime is set to latest version and click **Finish**.

**Step 2:** Locate and click on the **pom.xml** file that has been automatically created for you.

**Step 3:** Add the following components (**seen inside configuration**) to your pom.xml file to allow for deployment to cloudhub.  Afterwards, click **File-> Save All**.


	<plugins>
			<plugin>
				<groupId>org.mule.tools.maven</groupId>
				<artifactId>mule-maven-plugin</artifactId>
				<version>${mule.maven.plugin.version}</version>
				<extensions>true</extensions>
				  <configuration>
					<cloudHubDeployment>
					<muleVersion>4.2.2</muleVersion>
					<username>{your-username}</username>
					<password>{your-password}</password>
					<environment>Sandbox</environment>
					<applicationName>mule-linabel-application</applicationName>
					<workers>1</workers>
					<workerType>Micro</workerType>
					</cloudHubDeployment>
				</configuration>
			</plugin>
		</plugins>


**Step 4:** Locate the path of your mule project application via right-clicking mule project name and going to properties. Copy the location path.

	 






 
**Step 5:** Go to your command prompt cd to the project path.
```
Linabel$ cd /Users/Linabel/AnypointStudio/studio-workspace/mule-linabel-demo
```

**Step 6:** Deploy to cloudhub using the following command:
```
mule-linabel-demo Linabel$ mvn package deploy -DmuleDeploy
```
Output:

```
[INFO] --- mule-maven-plugin:3.3.5:deploy (default-deploy) @ mule-linabel-demo ---
[INFO] Deploying artifact mule-linabel-application
[INFO] Creating application: mule-linabel-application
[INFO] Starting application: mule-linabel-application
[INFO] Checking if application: mule-linabel-application has started
[INFO] Artifact mule-linabel-application deployed
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  02:10 min
[INFO] Finished at: 2020-04-17T13:27:16-07:00
[INFO] ------------------------------------------------------------------------
```

**Step 7:** Go to https://anypoint.mulesoft.com/cloudhub/#/console/home/applications to see your application deployed in cloudhub.


### Troubleshooting solutions:

Make sure you don’t have any **typos** in the pom.xml file.

**Error:** “The default workspace … is in use or cannot be created. Please choose a different one”.
**Solution:**
-	Go to commandline prompt an navigate to the workspace folder.
-	Delete the .lock file in the hidden .metadata directory.
-	Try re-opening workspace

```
Linabel$ cd /Users/Linabel/AnypointStudio/studio-workspace/.metadata
Linabel$ rm .lock
Linabel$ 
```
source: http://are-you-ready.de/blog/2016/09/21/eclipse-workspace-in-use/

**Error:** Caused by: org.mule.tools.client.core.exception.ClientException: 400 Bad Request: {"status":400,"message":"Object Store V1 is not supported for your org"}

**Solution:**
source: https://help.mulesoft.com/s/question/0D52T00004xJUgESAW/mule-4-cannot-deploy-mulesoft-application-to-cloudhub-using-mule-maven-plugin

#### FIN
