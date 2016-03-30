
## Sample Spring Boot REST app 
* See the `README.adoc` for spring readme, below is some more useful info. 
* cd into the 'initial' dir for the project (the `complete` dir has the original/un-modified tutorial src from spring). 
* The app can run either as Spring-boot application, or as regular .war file for deployment to an external server. 
* For .war deployments: 
  * The app has been successfully deployed to different servlet containers including Tomcat8 and IBM Liberty server. 
  * The app has been successfully deployed to IBM BlueMIX cloud (instructions below). 

## Build as .war 
* Install maven, set mvn proxy/settings.xml and run: 
```bash
cd initial
mvn clean
mvn package 
```

## To deploy this application in the IBM bluemix cloud 
* Bluemix cloud based on CloudFoundary 
* Download/install the 'cf' CLI tool to push/deploy apps to bluemix
* Create a new project (typically a war file, note you don't have to use bluemix git) 
* Set the local http_proxy and https_proxy vars if behind a proxy 
* The basic process is: a) cf login, b) set cf service region, c) configure cf app settings in 'manifest.yml', d) push to bluemix cloud, e) view/manage your deployed apps in bluemix hosting portal 

```bash
cd initial
cf.exe api https://api.eu-gb.bluemix.net
cf.exe login -u <your_ibm_bluemix_account_name> -p <yourpassword>  
vim manifest.yml #<edit config file for the service(s)/settings and webapp name in bluemix>
cf push # push to bluemix cloud
```


* Full example (note, ignore the deploy error - this worked when i cleared up some space on bluemix): 
```bash
[initial]$export http_proxy=http://wwwcache.dl.ac.uk:8080
[initial]$export https_proxy=http://wwwcache.dl.ac.uk:8080
[initial]$
[initial]$
[initial]$cf api https://api.eu-gb.bluemix.net
Setting api endpoint to https://api.eu-gb.bluemix.net...
OK


API endpoint:   https://api.eu-gb.bluemix.net (API version: 2.40.0)
Not logged in. Use 'cf.exe login' to log in.
[initial]$cf.exe login -u <yourbluemixIdAccount> -p <your password>
API endpoint: https://api.eu-gb.bluemix.net
Authenticating...
OK

Targeted org <your.organisation>

Targeted space dev



API endpoint:   https://api.eu-gb.bluemix.net (API version: 2.40.0)
User:           <yourdetails>
Org:            <yourdetails>
Space:          dev
[initial]$


[initial]$cf push
Using manifest file C:\Users\djm76\Documents\programming-vcs\java\spring-rest-sample\gs-rest-service\initial\manifest.yml

Creating app davesSpringWS1 in org <yourdetails> / space dev as <yourdetails>...
OK

Creating route davesSpringWS1.eu-gb.mybluemix.net...
OK

Binding davesSpringWS1.eu-gb.mybluemix.net to davesSpringWS1...
OK

Uploading davesSpringWS1...
Uploading app files from: C:\Users\djm76\Documents\programming-vcs\java\spring-rest-sample\gs-rest-service\initial\target\gs-rest-service-0.1.0.war
Uploading 493.6K, 91 files
Done uploading
OK

Starting app davesSpringWS1 in org <yourdetails> / space dev as <yourdetails>...
FAILED
Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.

```





