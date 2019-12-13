---
page_type: sample
description: This sample demonstrates a Java web application authenticating via AD FS with the option to access a secured API resource.
languages:
  - java
products:
  - AD FS 2016
---

# Integrating ADFS into a Java web application

## About this sample

### Overview

This sample application was modified to work with AD FS from the following sample application: https://github.com/AzureAD/azure-activedirectory-library-for-java

1. The Java web application uses the Active Directory Authentication Library for Java(ADAL4J) to obtain a JWT access token from Active Directory Federation Services (AD FS):
2. The access token is used as a bearer token to authenticate the user when calling a secured API (TODO)

### Scenario

This sample shows how to build a Java web app(confidential client) that uses OpenID Connect to sign-in users from an AD FS tenant using ADAL4J. 

## How to run this sample

To run this sample, you'll need:

- Working installation of Java and Maven
- Tomcat or any other J2EE container solution
- An Internet connection
- Active Directory Federation Services (AD FS) tenant. 
- A user account in your AD FS tenant. 

### Step 1: Download Java (8 and above) for your platform

To successfully use this sample, you need a working installation of [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html) and [Maven](https://maven.apache.org/).

### Step 2:  Clone or download this repository

From your shell or command line:

- `git clone https://dajon0708@dev.azure.com/dajon0708/SamlPoc/_git/SamlPoc`

### Step 3:  Register the sample with your AD FS tenant

This has been completed by an administrator for the sample application.

#### Register the app app (Webapp-Openidconnect)

1. The **Redirect URIs** has been set to `https://localhost:8443/adal4jsample/secure/aad`
1. The Client Id and Client Secret has been generated, those values will be used in step 4.

### Step 4:  Configure the sample to use your Azure AD tenant

Open `web.xml` in the webapp/WEB-INF/ folder. Because we are working with ADFS we do not need to fill in the tenant name, instead Replace the "Authority" tag with the AD FS endpoint 'YOUR_CLIENT_ID' with the Application Id and 'YOUR_CLIENT_SECRET' with the key value noted.

### Step 5: Package and then deploy the adal4jsample.war file.

- `$ mvn compile -DgroupId='com.microsoft.azure' -DartifactId=adal4jsample -DinteractiveMode=false`

- `$ mvn package`

This will generate a `adal4jsample.war` file in your /targets directory. Deploy this war file using Tomcat or any other J2EE container solution. 

*Important* You must enable HTTPS to listent to port 8433, that is the where ADFS is configured to accept callbacks from. For more information on Tomcat SSL/TLS configuration: https://tomcat.apache.org/tomcat-7.0-doc/ssl-howto.html


To deploy on Tomcat container
- Navigate to your Tomcat installation (default installation on windows is `C:\Program Files\Apache Software Foundation\Tomcat`)
- copy the `adal4jsample.war` file to the Tomcat\webapps folder 
- Start the Tomcat server. One way to do this is by opening the Monitor Tomcat app, clicking on `start` in the `General` tab

This WAR will automatically be hosted at `https://<yourserverhost>:<yourserverport>/adal4jsample/`


Example: `https://localhost:8433/adal4jsample/`

### You're done!

- Click on "Log in using OpenID Connect" to start the process of logging in.
- Select Active Directory
- Select "Sign in using an x.503 certificate" username/password should work as well.
- Select a valid certificate and enter your pin
- You should be redirected to a page showing basic profile attributes of the user signed in, such as first name and last name.
- You should also be presented with a JWT token that can be parsed to extract custom claims.
- Optionally the access token received can be used to call a secured API, using it as a bearer token. 


## More information

For more information, see ADAL4J [conceptual documentation](https://github.com/AzureAD/azure-activedirectory-library-for-java/wiki)

For more information about how OAuth 2.0 protocols work in this scenario and other scenarios, see [Authentication Scenarios for Azure AD](http://go.microsoft.com/fwlink/?LinkId=394414).
