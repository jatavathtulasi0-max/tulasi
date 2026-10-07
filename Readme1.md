EXPERIMENT NO. 6

AIM: Explore Docker commands for content management.
Introduction

Containerization is a technology that has revolutionised the way applications are developed, deployed, and managed in the modern IT landscape. It provides a standardised and efficient way to package, distribute, and run software applications and their dependencies in isolated environments called containers.
Containerization technology has gained immense popularity, with Docker being one of the most well-known containerization platforms. This introduction explores the fundamental concepts of containerization, its benefits, and how it differs from traditional approaches to application deployment.

Programs:
Program #1: Run an Hello-World image in Docker

$ docker version	//checks docker version
$ docker pull hello-world	//pulls hello-world image from docker hub
$ docker run hello-world	//runs hello-world image
$ docker ps –a	// lists all containers
$ docker images	// lists all images


Program #2: Run an Ubuntu image in Docker container named  “MyContainerA” and execute some shell commands

$ docker version	//checks docker version
$ docker pull ubuntu:latest	//pulls ubuntu image from docker hub


// runs ubuntu image in container named MyContainerA and opens shell script


$ docker run -it --name MyContainerA ubuntu -- /bin/bash root @[containerid]... $ whoami
root @... $ ls
root @... $ mkdir mydir root @... $ cd mydir
root @... $ echo “Hello from MVSR” > sample.txt root @... $ ls
root @... $ pwd
root @... $ ping www.google.com root @... $ exit
$ docker ps –a	// lists all containers
$ docker images	// lists all images
$ docker logs MyContainerA	// log of container

EXPERIMENT NO. 7

AIM: Develop a simple containerized application using Docker. Program #1: HTML docker image
Steps to create Web-HTML docker image
	Login to super user using sudo su command
o	$ sudo su
	Create a directory HtmlDemo and create a HTML file and Docker file inside it.
o	$ mkdir HtmlDemo
o	$ cd HtmlDemo
o	vi index.html
<html>
<head>
<title> Hello Page</title>
</head>
<body>
<<h1> Welcome to HTML Docker </h1>
</body>
</html>
o	vi Dockerfile
FROM nginx:latest
WORKDIR /usr/share/nginx/html COPY ./index.html .
EXPOSE 80
	Build and run the Docker image
o	$ docker build –t htmlimage .
o	$ docker run -it htmlimage
	Login to Docker hub and push the image to your account
o	$ docker login -u [Dockerhubusername]
Eg: $ docker login -u sowjanyajindam

o	$ docker tag imagename Dockerhubusername/imagename Eg: $ docker tag htmlimage sowjanyajindam/htmlimage

o	$ docker push Dockerhubusername/imagename Eg: $ docker push sowjanyajindam/htmlimage

	Pull the code from Docker hub and execute
o	$  docker pull sowjanyajindam/htmlimage
o	$ docker run -it sowjanyajindam/htmlimage
Program # 2: JAVA docker image
Steps to create JAVA docker image
	Login to super user using sudo su command
o	$ sudo su
	Create a directory JavaDemo and create a JAVA file and Docker file inside it.
o	$ mkdir JavaDemo
o	$ cd JavaDemo
o	vi Hello.java
class Hello
{
public static void main(String args[])
{
System.out.println("Hello Docker from java");
}
}

o	vi Dockerfile
FROM openjdk:11 WORKDIR /app COPY ./Hello.java . RUN javac Hello.java
CMD ["java", "Hello"]
	Build and run the Docker image
o	$ docker build –t javaimage .
o	$ docker run -it javaimage
	Login to Docker hub and push the image to your account
o	$ docker login -u [Dockerhubusername]
Eg: $ docker login -u sowjanyajindam

o	$ docker tag imagename Dockerhubusername/imagename Eg: $ docker tag javaimage sowjanyajindam/javaimage

o	$ docker push Dockerhubusername/imagename Eg: $ docker push sowjanyajindam/javaimage

	Pull the code from Docker hub and execute
o	$ docker pull sowjanyajindam/ javaimage
o	$ docker run -it sowjanyajindam/ javaimage

EXPERIMENT NO. 8

AIM: Dockerize the Student Registration Application from the Program 1 and push the code to GITHUB and DOCKERHUB
Program:
Dockerization Steps:
	Login to super user using sudo su command
o	$ sudo su
	Check whether docker and docker compose are installed.
o	$ docker version
o	$ docker-compose version
	Create a directory StudReg and code file, docker and docker compose yaml file inside it.
o	$ mkdir StudReg
o	$ cd StudReg
o	Add streg.jpg to the directory
o	vi stud.html
<html>
<head>
<link href="studreg.css" rel="stylesheet" />
</head>

<body>
<img src="streg.jpg" alt="stud reg image" class="center">
<h1> DevOps Lab</h1>
<h2> Student Registration Form</h1>

<form action = "http://127.0.0.1:8081/process_get" method = "GET">

<table border="5" align="center" cellspacing="10" cellpadding="10" >

<tr>
<td>Name</td><td><input type="text" name="sname"></td>
</tr>
<tr>
<td>Contact Number</td>
<td><input type="text" name="scon"></td>
</tr>
<tr>
<td>Gender</td>
<td><input type="radio" name="g">Male
<input type="radio" name="g">Female</td>
</tr>

<tr>
<td>Address</td>
<td><textarea rows="5" cols="15" name="sadd"></textarea></td>
</tr>

<tr>
<td>Hobbies</td>
<td><input type="checkbox" name="shob">Singing
<input type="checkbox" name="shob">Travelling
<input type="checkbox" name="shob">Reading novels
</td>
</tr>

<tr>
<td>Skillset</td>
<td><input type="checkbox" name="sss">C
<input type="checkbox" name="sss">Python
<input type="checkbox" name="sss">Java
</td>
</tr>


<tr>
<td>Highest Qualification</td>
<td><select name="shq">
<option><--SELECT--></option>
<option>Ph.D</option>
<option>M.E/M.Tech</option>
<option>B.E/B.Tech</option>
<option>Diploma</option>
<option>Inter</option>
<option>SSC</option>
</select>
</td>
</tr>
<td>District</td>
<td><select name="sdis">
<option>--SELECT--></option>
<option>Adilabad</option>
<option>Zaheerabad</option>
</select>
</td>
</tr>

<tr>
<td><input type="submit" name="submit" value="Register"></td>
<td><input type="reset" value="Clear"></td>
</tr>


</table>
</form>
</body>
</html>


vi studreg.css

h1{

color:green;
text-align:center;
}

h2{

color:blue;
text-align:center;
}

p{
color:red;
}

table{
background-color: cyan;
}
td{
color:red;
font-size:24px;
}
input
{
color:blue; font-size:24px;
text-align : center;
}
select
{
color:blue; font-size:24px;
text-align : center;
}
.center { display: block;
margin-left: auto; margin-right: auto; width: 50%;
}

vi studregnode.js

var express = require('express'); var app = express();
app.use(express.static('public')); app.get('/studreg.html', function (req, res) {
res.sendFile(  dirname + "/" + "studreg.html" );
})

app.get('/process_get', function (req, res) {
// Prepare output in JSON format response = {
stud_name:req.query.sname, stud_contact:req.query.scon, stud_gender:req.query.g, stud_address:req.query.sadd, stud_hobbies:req.query.shob, stus_skillset:req.query.sss, stud_highest_qualification:req.query.shq, stud_district:req.query.sdis
};
console.log(response); res.end(JSON.stringify(response));
})

var server = app.listen(8081, function () { var host = server.address().address
var port = server.address().port

console.log("Example app listening at http://%s:%s", host, port)
})


vi Dockerfile

FROM node:14 WORKDIR /app
COPY package*.json . RUN npm install
RUN npm install express COPY . /app
EXPOSE 8081
CMD ["node", "studregnode.js"]

vi studreg-docker-compose.yaml

version: "3.0" services:
myweb:
image: node:14 build: .

container_name: nodecons restart: always
ports:
- "8081:8081"
expose:
- "8081"
	Execute the program in local environment
o	$ apt-get update
o	$ apt install nodejs
o	$ apt install npm
o	$ npm install -g express
o	$  node –v
o	$  npm –v
o	$  npm init
o	$  node studregnode.js

	Build and run the Docker image
o	$ docker build –t studregimage .
o	$ docker run --rm -it -p 8081:8081 --name nodecon studregimage

	Go to https:\\ localhost:8081\stud.html to see the output
	Build and run the Docker images using Docker Compose
o	$ docker-compose -f studreg-docker-compose.yaml up -d
	Login to GITHUB and create a new GIT repository name StudRegRepo and copy the URL
	Push the code to GITHUB
o	$ git --version
o	$ git config --global user.name “sowjanya”
o	$ git config --global user.email sowjanya@gmail.com
o	$ git remote add origin https://github.com/sowjanya/StudRegRepo.git
o	$ git config --list
o	$ git init
o	$ git status
o	$ git add .
o	$ git commit -m "1st commit files added"
o	$ git branch -M main
o	$ git status
o	$ git push -u origin main

Go to remote repository and check whether project is uploaded on github.

	Login to Docker hub and push the image to your account
o	$ docker login -u [Dockerhubusername]
Eg: $ docker login -u sowjanyajindam

o	$ docker tag imagename Dockerhubusername/imagename Eg: $ docker tag nodeimage sowjanyajindam/studregimage

o	$ docker push Dockerhubusername/imagename Eg: $ docker push sowjanyajindam/studregimage

	Pull the code from Docker hub and execute
o	$  docker pull sowjanyajindam/studregimage
o	$ docker run -it sowjanyajindam/studregimage

Go to https:\\ localhost:8081\stud.html to see the output

EXPERIMENT NO. 9
AIM: Integrate Kubernetes and Docker
Introduction:
Container orchestration is a critical component in modern application deployment, allowing you to manage, scale, and maintain containerized applications efficiently.
Kubernetes is a popular container orchestration platform that automates many tasks associated with deploying, scaling, and managing containerized applications.

Kubernetes, often abbreviated as K8s, is an open-source container orchestration platform designed to automate the deployment, scaling, and management of containerized applications. Developed by Google and later donated to the Cloud Native Computing Foundation (CNCF), Kubernetes has become the de facto standard for container orchestration in modern cloud-native application development.
Program:
Installation of kubernetes 
sudo su
docker version ( install docker if not available)
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64 minikube version
minikube start --driver=docker minikube kubectl -- get po -A snap install kubectl --classic kubectl version
minikube start --force
minikube addons enable ingress
minikube start --nodes 2 -p multinode-demo minikube dashboard
Kubernetes Commands:
Cluster Management
	Display the Kubernetes version running on the client and server
kubectl version

	Display endpoint information about the master and services in the cluster
kubectl cluster-info

	Get the configuration of the cluster
kubectl config view

	List the API resources that are available
kubectl api-resources

	List the API versions that are available
kubectl api-versions

	List everything
kubectl get all --all-namespaces

Namespaces
	Create namespace <name>
kubectl create namespace <namespace_name>
	List one or more namespaces
kubectl get namespace <namespace_name>
	Display the detailed state of one or more namespace
kubectl describe namespace <namespace_name>
	Delete a namespace
kubectl delete namespace <namespace_name>
	Edit and update the definition of a namespace
kubectl edit namespace <namespace_name>
	Display Resource (CPU/Memory/Storage) usage for a namespace
kubectl top namespace <namespace_name>

Nodes
	List one or more nodes
kubectl get node

	Delete a node or multiple nodes
kubectl delete node <node_name>

	Display Resource usage (CPU/Memory/Storage) for nodes
kubectl top node

	Resource allocation per node
kubectl describe nodes | grep Allocated -A 5

	Pods running on a node
kubectl get pods -o wide | grep <node_name>

	Add or update the labels of one or more nodes
kubectl label node
Pods
	List one or more pods
kubectl get pod
kubectl get pods -o wide kubectl get pods –o=yaml kubectl get pods –o=json
kubectl get pods -n=[namespace_name]


	Delete a pod
kubectl delete pod <pod_name>

	Display the detailed state of a pods
kubectl describe pod <pod_name>

	Create a pod
kubectl create pod <pod_name>

	Execute a command against a container in a pod
kubectl exec <pod_name> -c <container_name> <command>

	Get interactive shell on a a single-container pod
kubectl exec -it <pod_name> /bin/sh

	Display Resource usage (CPU/Memory/Storage) for pods
kubectl top pod

	Add or update the annotations of a pod
kubectl annotate pod <pod_name> <annotation>

	Add or update the label of a pod
kubectl label pod <pod_name>

Deployments
	List one or more deployments
kubectl get deployment

	Display the detailed state of one or more deployments
kubectl describe deployment <deployment_name>

	Edit and update the definition of one or more deployment on the server
kubectl edit deployment <deployment_name>

	Create one a new deployment
kubectl create deployment <deployment_name>

	Delete deployments
kubectl delete deployment <deployment_name>

	See the rollout status of a deployment
kubectl rollout status deployment <deployment_name>

ReplicaSets
	List ReplicaSets
kubectl get replicasets

	Display the detailed state of one or more ReplicaSets
kubectl describe replicasets <replicaset_name>

	Scale a ReplicaSet
kubectl scale --replicas=[x]

Logs
	Print the logs for a pod
kubectl logs <pod_name>

	Print the logs for the last hour for a pod
kubectl logs --since=1h <pod_name>

	Get the most recent 20 lines of logs
kubectl logs --tail=20 <pod_name>

	Get logs from a service and optionally select which container
kubectl logs -f <service_name> [-c <$container>]
	Print the logs for a pod and follow new logs
kubectl logs -f <pod_name>

	Print the logs for a container in a pod
kubectl logs -c <container_name> <pod_name>

	Output the logs for a pod into a file named „pod.log‟
kubectl logs <pod_name> pod.log

	View the logs for a previously failed pod
kubectl logs --previous <pod_name>

Manifest Files
	Apply a configuration to an object by filename or stdin. Overrides the existing configuration.
kubectl apply -f manifest_file.yaml

	Create objects
kubectl create -f manifest_file.yaml

	Create objects in all manifest files in a directory
kubectl create -f ./dir

	Create objects from a URL
kubectl create -f „url‟

	Creating a pod using data in a file named newpod.json.
kubectl create -f ./newpod.json

	Delete an object
kubectl delete -f manifest_file.yaml

Secrets
	Create a secret
kubectl create secret
	List secrets
kubectl get secrets
	List details about secrets
kubectl describe secrets

	Delete a secret
kubectl delete secret <secret_name>

Services
	List one or more services
kubectl get services

	Display the detailed state of a service
kubectl describe services
	Expose a replication controller, service, deployment or pod as a new Kubernetes service
kubectl expose deployment [deployment_name]

	Edit and update the definition of one or more services
kubectl edit services

There are four types of services that Kubernetes supports: ClusterIP, NodePort, LoadBalancer, Ingress


Workflow in Kubernetes 
 

EXPERIMENT NO. 10

AIM: Automate the process of running containerized application developed in program 7 using Kubernetes.
Program # 1: Create an nginx and mongo deployment and run some kubectl commands
Step 1: create nginx deployment and check status
	$ kubectl create deployment nginx-depl –image=nginx
	$ kubectl get deployments
	$ kubectl get nodes
	$ kubectl get pods
	$ kubectl get replicaset

Step 2: Execute the deployment and run some commands in nginx
	$ kubectl get pods ( copy pod id and use it in next command to run the pod)
	$ kubectl exec -it nginx-depl-85zrbt9 -- /bin/bash
	root@nginxid..$ ls
	root@nginxid..$ mkdir mydir
	root@nginxid..$ echo “Hello nginx” > sample.txt
	root@nginxid..$ ls
	root@nginxid..$ exit
Step 3: Edit deployment, change replicaset and check log

	$ kubectl edit deployment nginx-depl
( in opened file make some changes to version, replicas, namespace…)
	$ kubectl get replicasets
	$ kubectl scale deployment/nginx-depl --replicas=5
	$ kubectl get replicasets
	$ kubectl get pods
	$ kubectl logs [nginx-depl pod ID]
Step 4: create mongo deployment and check status

	$ kubectl create deployment mongo-depl --image=mongo
	$ kubectl get deployments
	$ kubectl get pods
	$ kubectl get replicaset

Step 5: Execute the mongo deployment and run some commands in mongo
	$ kubectl get pods ( copy pod id and use it in next command to run the pod)
	$ kubectl exec -it mongo-depl-85shtudf -- /bin/bash
	root@mongo-depl-id..# show databases;
# db.student.insert( , name : “Sunny”, age: 20, dept : “IT” - );
# db.student.insert( , name : “Sony”, age: 22, gender : “Female”, dept : “IT” - ); # db.student.find();
# db.student.delete( , name : “Sunny” - ); # db.student.find();
# show collections; # exit
Step 6: Delete deployments
	$ kubectl delete deployment nginx-depl
	$ kubectl get pods
	$ kubectl delete deployment mongo-depl
	$ kubectl get pods

Program # 2: Create an nginx deployment using manifest (YAML) files

Step 1: create a yaml file for nginx deployment and apply it
	$ touch nginx-depl.yaml
	$ vi nginx-depl.yaml
 
	$ kubectl apply -f nginx-depl.yaml
	$ kubectl get deployments
	$ kubectl get pods
	$ kubectl get replicaset
	$ kubectl describe deployment nginx-deployment
0r
	$ kubectl create namespace myspace
	$ kubectl apply -f nginx-depl.yaml -n=myspace
	$ kubectl get deployments -n=myspace

EXPERIMENT NO. 11

AIM: Install and Explore Selenium for automated testing.
Introduction to Selenium Automation Testing:
Selenium is one of the most widely used open source Web UI (User Interface) automation testing suite.It was originally developed by Jason Huggins in 2004 as an internal tool at Thought Works. Selenium supports automation across different browsers, platforms and programming languages.

Selenium can be easily deployed on platforms such as Windows, Linux, Solaris and Macintosh. Moreover, it supports OS (Operating System) for mobile applications like iOS, windows mobile and android.

Selenium supports a variety of programming languages through the use of drivers specific to each language.Languages supported by Selenium include C#, Java, Perl, PHP, Python and Ruby.Currently, Selenium Web driver is most popular with Java and C#. Selenium test scripts can be coded in any of the supported programming languages and can be run directly in most modern web browsers. Browsers supported by Selenium include Internet Explorer, Mozilla Firefox, Google Chrome and Safari.
 
Selenium can be used to automate functional tests and can be integrated with automation test tools such as Maven, Jenkins, & Docker to achieve continuous testing. It can also be integrated with tools such as TestNG, & JUnit for managing test cases and generating reports.

One disadvantage of Selenium automation testing is that it works only for web applications, which leaves desktop and mobile apps out in the cold.

Selenium consists of a set of tools that facilitate the testing process.
 
Fig: Selenium suite
1.	Selenium IDE
Shinya Kasatani developed the Selenium Integrated Development Environment (IDE) in 2006. Conventionally, it is an easy-to-use interface that records the user interactions to build automated test scripts. It is a Firefox or Chrome plugin, generally used as a prototyping tool. It was mainly developed to speed up the creation of automation scripts.

IDE ceased to exist in August 2017 when Firefox upgraded to the new Firefox 55 version, which no longer supported Selenium IDE. Applitools rewrote the old Selenium IDE and released a new version recently. The latest version came with several advancements, such as:

	Reusability of test scripts
	Debugging test scripts
	Selenium side runner
	Provision for control flow statements
	Improved locator functionality

Installing IDE:
Step 1- Open the Firefox browser
Step 2- Click on the menu in the top right corner Step 3- Click on Add-ons in the drop-down box.
Step 4- Click on Find more add-ons and type “Selenium IDE” Step 5- Click on Add to Firefox

2.	Selenium Remote Control (RC)
Paul Hammant developed Selenium Remote Control. Selenium RC is a server written in Java that makes provision for writing application tests in various programming languages like Java, C#, Perl, PHP, Python, etc. The RC server accepts commands from the user program and passes them to the browser as Selenium-Core JavaScript commands.
3.	Selenium WebDriver
Developed by Simon Stewart in 2006, Selenium WebDriver was the first cross-platform testing framework that could configure and control the browsers on the OS level. It served as a programming interface to create and run test cases.

Unlike Selenium RC, WebDriver does not require a core engine like RC and interacts natively with the browser applications. WebDriver also supports various programming languages like Python, Ruby, PHP, and Perl. It can also be integrated with frameworks like TestNG and JUnit for Selenium automation testing management.

Steps for Selenium WebDriver installation :

1.	Download and Install Java 8 or higher version - Install the latest version of the Java development kit.
2.	Download and configure Eclipse or any Java IDE of your choice
3.	Download Selenium WebDriver Java Client
1.	Navigate to the official Selenium page.
2.	Scroll down through the web page and locate Selenium Client and WebDriver Language Bindings.
3.	Click on the "Download" link of Java Client Driver . Unzip the file in a directory. It consists of the Jar files required to configure Selenium WebDriver in the IDE.
4.	Download the Browser driver - The automation scripts must be compatible with any browser. Every browser supported by Selenium comes with its driver files.
5.	Configure Selenium WebDriver - The final step is to configure the Selenium WebDriver with the Eclipse IDE. In simple terms, we create a new Java project to build our test script.


4.	Selenium Grid
Selenium Grid was developed by Patrick Lightbody to minimize the execution time of Selenium automation testing. Selenium Grid allows the parallel execution of tests on different browsers and different operating systems, facilitating parallel execution. Grid is exceptionally flexible and is integrated with other suite components for simultaneous performance.

The Grid consists of a hub connected to several nodes. It receives the test to be executed along with information about the operating system and browser to be run on. The Grid then picks a node that conforms to the requirements (browser and platform) and passes the test to that node. The node now runs the browser and executes the Selenium commands within it.

EXPERIMENT NO. 12

AIM: Write a simple program in JavaScript and perform testing using Selenium. Program # 1: Write a JavaScript program to open Google website in the browser
Step 1: Create directory and add file.
o	$ mkdir googleDemo
o	$ cd googleDemo
o	vi app.js
const {Builder, By, Key} = require("selenium-webdriver");

async function example(){
let driver = await new Builder().forBrowser("chrome").build(); await driver.get("https://www.google.com/"); console.log("browser opened");
await driver.quit();
}
example()

Step 2: Initialize the project and execute it
Execution Steps for Selenium:

	node -v
// check whether node is installed. If not, install using below commands.
// sudo apt-get update
//sudo apt install nodejs

	npm -v
// check whether npm is installed. If not, install using below commands.
//sudo apt install npm

	npm init	// Initilaze the node package
	npm install selenium-webdriver	// add selenium web driver as dependency
	npm init	//check out for addition of selenium dependency
	node app.js	//execute the program
Note: Selenium web drivers run only in Higher versions of node, so see to that node version 16 and above are installed.

For installation of higher version of node
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash source ~/.bashrc
nvm list-remote nvm install v16.14.0
Program # 2: Write a JavaScript program for login validation application and  test it using Selenium.

Step 1: Create directory and add file.
o	$ mkdir myloginDemo
o	$ cd myloginDemo
o	vi login.html
<html>
<head>
<title> Login Page</title>
<script language="javascript">

function validate()
{
var u=document.f1.u.value; var p=document.f1.p.value;

if(u=="MVSREC" && p=="ITD")
{
window.open("loginsuccess.html");
}
else
{
window.open("loginfail.html");
}
}
</script>
</head>
<body>
<form name="f1">
<h1 align="center" style="color:blue">Login Page</h1>
<table align="center" bgcolor="pink">
<tr>


</tr>
<tr>

</tr>
<tr>


</tr>
</table>
</form>
</body>
</html>
<td>UserId</td>
<td><input type="text" name="u" id="un"></td>


<td>Password</td>
<td><input type="password" name="p" id="pw"></td>

<td><input type="button" value="Signin" id="s" onclick="validate()"></td>
<td><input type="reset" value="Reset id="r"></td>

o	vi loginsucess.html

<html>
<head>
<title> Success </title>
</head>
<body>
<h1 align="center" style="color:red"> Login Succeess</h1>
</body>
</html>


o	vi loginfail.html
<html>
<head>
<title> Fail </title>
</head>
<body>

<h1 align="center" style="color:red"> Login Failed</h1>
</body>
</html>
 
o	vi mylogin.js
const { Builder, By, until } = require("selenium-webdriver"); const assert = require("assert");

async function loginTest() {
// launch the browser

let driver = await new Builder().forBrowser("chrome").build(); try {
await driver.get("file:///home/mvsr/myloginDemo/login.html"); await driver.findElement(By.id("un")).sendKeys("MVSREC"); await driver.findElement(By.id("pw")).sendKeys("ITD");
await driver.findElement(By.id("s")).click(); const title = await driver.getTitle();
assert.strictEqual(title,"Login Page"); console.log("success");

} finally {
await driver.quit();
}
}
loginTest();
Step 2: Initialize the project and execute it
Execution Steps for Selenium:

	node -v
// check whether node is installed. If not, install using below commands.
// sudo apt-get update
//sudo apt install nodejs

	npm -v
// check whether npm is installed. If not, install using below commands.
//sudo apt install npm

	npm init	// Initilaze the node package
	npm install selenium-webdriver	// add selenium web driver as dependency
	npm init	//check out for addition of selenium dependency
	node mylogin.js	//execute the program




EXPERIMENT NO. 13

AIM: Write a simple program in Java and perform testing using Selenium.
Program # 1: Write a Java program in eclipse IDE to open Google website in the browser

Step 1: Download selenium-server-standalone-3.141.59.jar and chromedriver suitable for you chrome browser

Step 2: Open Eclipse IDE and create a new Project
	Provide a project name and select the JRE that you wish to use. It is advisable to use the default JRE. Select it and click on finish.
	On the project name, right click and add new package (loginval)
	Now, right click on package name and add new java class.(Loginval)
	To do that, Right-click on Src folder>>New>>Class
	Write the following code.

package loginval;
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.*;


public class Loginval {
public static void main(String[] args) throws Exception{ System.setProperty("webdriver.chrome.driver","//home/mvsr/seleniumlib/chromedriver"); WebDriver driver = new ChromeDriver();
driver.get("http://www.google.com/”); Thread.sleep(5000); // Let the user actually see something!

WebElement searchBox = driver.findElement(By.name("q")); searchBox.sendKeys("ChromeDriver");
searchBox.submit();

Thread.sleep(5000); // Let the user actually see something! driver.quit();
}
}
Step 3: Add JAR files
	The next and most crucial step is to add the downloaded JAR file [Step 1].
	To add JAR file, right-click on the Project>>Build Path>>Configure Build Path.
	Select libraries and then Add External JARs.
	Open the folders in which you’ve saved your JAR files and select the executable JAR file. Click on open to add it.
	Click on the libs folder>> Select the files>> Open
	Once you’re done adding the library files, click on Apply and Close.
Step 4: Run the Java Program

	Click on Run>>Run As>>Java Application >> Loginval

Step 5: Output

	Chrome browser should open automatically and navigate to www.google.com and search for the word chrome driver and display results.

EXPERIMENT NO. 14

AIM: Develop test cases for the above containerized application using selenium.
Case Study #1: Develop a Web-Application for Calculator, Write test cases for different operations and test it using Selenium. Dockerize the program and push the containerized application code to GitHub and DockerHub.
Program: Steps
	Login to super user using sudo su command
o	$ sudo su
	Check whether Git, node and docker are installed.
o	$ git version
o	$ docker version
o	$ node –v
o	$ npm –v
	Create a directory StudReg and code file, docker and docker compose yaml file inside it.
o	$ mkdir Calculator
o	$ cd Calculator
o	vi index.html
<html>
<script language="javascript"> var prev,oper;
function num(s)
{
var n=parseInt(document.f1.t1.value); var sum=(n*10)+s; document.f1.t1.value=sum;
}
function op(k)
{
oper=k; prev=parseInt(document.f1.t1.value); document.f1.t1.value=0;
}
function mod()
{
a=parseInt(document.f1.t1.value); b=Math.floor(a/10); document.f1.t1.value=b;
}

function eq()
{
curr=parseInt(document.f1.t1.value); switch(oper)
{
case 1: var result=prev+curr;break; case 2: var result=prev-curr;break; case 3: var result=prev*curr;break; case 4: var result=prev/curr;break;
case 5: var result=prev%curr;break;
}

document.f1.t1.value=result;
}
</script>

<body >
<form name="f1">
<h1 align="center">Basic Calculator</h1>
<table align="center" bgcolor="cyan" cellspacing="10" cellpadding="20">

<tr><td colspan="4"><input id = "res" type="text" name = "t1" value="0" size="50"></tr>
<tr><td><input id = "1" type="button" value=" 1 " onclick="num(1)">
<td><input id = "2" type="button" value=" 2 " onclick="num(2)">
<td><input id = "3" type="button" value=" 3 " onclick="num(3)">
<td><input id = "add" type="button" value=" + " onclick="op(1)">
</tr>

<tr>
<td><input id = "4" type="button" value=" 4 " onclick="num(4)">
<td><input id = "5" type="button" value=" 5 " onclick="num(5)">
<td><input id = "6" type="button" value=" 6 " onclick="num(6)">
<td><input id = "sub" type="button" value=" - " onclick="op(2)">
</tr>
<tr>
<td><input id = "7" type="button" value=" 7 " onclick="num(7)">
<td><input id = "8" type="button" value=" 8 " onclick="num(8)" >
<td><input id = "9" type="button" value=" 9 " onclick="num(9)">
<td><input id = "mul" type="button" value=" * " onclick="op(3)">
</tr>
<tr>
<td><input id = "0" type="button" value=" 0 " onclick="num(0)">
<td><input id = "div" type="button" value=" / " onclick="op(4)">
<td><input id = "mod" type="button" value=" % " onclick="op(5)">
<td><input id = "equ" type="button" value=" = " onclick="eq()">
</tr>
<tr>
<td colspan="2"><input id = "c" type="reset" value=" c " ><td>
<input id = "bs" type="button" value=" <--- " onclick="mod()">
</tr>

</table>
</form>
</body>
</html>


	vi calculatortest.js
const { Builder, By , util } = require("selenium-webdriver"); const assert = require("assert");
async function calciTest() {

// launch the browser

let driver = await new Builder().forBrowser("chrome").build(); try {
await driver.get("file:///home/mvsr/Calculator/index.html"); await driver.sleep(2000);
await driver.findElement(By.id("5")).click(); await driver.findElement(By.id("add")).click(); await driver.findElement(By.id("8")).click(); await driver.findElement(By.id("equ")).click(); await driver.sleep(2000);

const value = await driver.findElement(By.name("t1")).getAttribute("value"); console.log(" answer is " + value);
await driver.sleep(2000); assert.equal(value,'13');
console.log(" Addition success");

await driver.findElement(By.id("c")).click(); await driver.findElement(By.id("5")).click(); await driver.findElement(By.id("sub")).click(); await driver.findElement(By.id("2")).click(); await driver.findElement(By.id("equ")).click(); await driver.sleep(2000);
const v1 = await driver.findElement(By.name("t1")).getAttribute("value"); console.log(" answer is " + v1);
await driver.sleep(2000); assert.equal(v1,'3');
console.log(" Subtraction success");

await driver.findElement(By.id("c")).click(); await driver.findElement(By.id("5")).click(); await driver.findElement(By.id("mul")).click(); await driver.findElement(By.id("2")).click(); await driver.findElement(By.id("equ")).click(); await driver.sleep(2000);

const v2 = await driver.findElement(By.name("t1")).getAttribute("value"); console.log(" answer is " + v2);
await driver.sleep(2000); assert.equal(v2,'10');
console.log(" Multiplication success");

await driver.findElement(By.id("c")).click(); await driver.findElement(By.id("6")).click(); await driver.findElement(By.id("div")).click(); await driver.findElement(By.id("2")).click(); await driver.findElement(By.id("equ")).click(); await driver.sleep(2000);

const v3 = await driver.findElement(By.name("t1")).getAttribute("value"); console.log(" answer is " + v3);
await driver.sleep(2000); assert.equal(v3,'3');
console.log(" Division success");

} finally {
await driver.quit();
}
}
calciTest();


	vi Dockerfile
FROM node:16.14.0
WORKDIR /app
COPY package*.json . RUN npm install COPY . /app
CMD ["node" , "calculatortest.js"]

	vi calci-docker-compose.yaml
version: "3.0" services:
myweb:
image: node:16.14.0 build: .
container_name: calcicons restart: always
ports:
- "8081:8081"
expose:
- "8081"
	Execute the program in local environment
o	$ apt-get update
o	$ apt install nodejs
o	$ apt install npm
o	$ npm install -g express
o	$  node –v
o	$  npm –v
o	$  npm init
o	$  npm install selenium-webdriver	// add selenium web driver as dependency
o	$  npm init
o	$  node calculatortest.js

	Build and run the Docker image
o	$ docker build –t calciimage .
o	$ docker run --rm -it -p 8081:8081 --name calcicon calciimage

	Go to https:\\ localhost:8081\index.html to see the output
	Build and run the Docker images using Docker Compose
o	$ docker-compose -f calci-docker-compose.yaml up -d

	Create a Kubernetes Deployment YAML file (calci-app-deployment.yaml) to deploy the web application:

calci-app-deployment.yaml

apiVersion: apps/v1 kind: Deployment metadata:
name: calci-app-deployment
spec:

replicas: 1 # Number of pods to create selector:
matchLabels:
app: calci-webapp # Label to match pods
template:
metadata:
labels:



app: calci-webapp # Label assigned to pods
spec:
containers:
-	name: calci-webapp-container
image: calciimage:latest # Docker image to use ports:
-	containerPort: 80 # Port to expose
	Apply the deployment configuration to your Kubernetes cluster:

$ kubectl apply -f calci-app-deployment.yaml
	Check the status of your pods:
$ kubectl get deployments
$ kubectl get pods
$ kubectl describe deployment my-web-app-deployment
	Login to GITHUB and create a new GIT repository name CalculatorRepo and copy the URL
	Push the code to GITHUB
o	$ git --version
o	$ git config --global user.name “sowjanya”
o	$ git config --global user.email sowjanya@gmail.com
o	$ git remote add origin https://github.com/sowjanya/CalculatorRepo.git
o	$ git config --list
o	$ git init
o	$ git status
o	$ git add .
o	$ git commit -m "1st commit files added"
o	$ git branch -M main
o	$ git status
o	$ git push -u origin main

Go to remote repository and check whether project is uploaded on github.

	Login to Docker hub and push the image to your account
o	$ docker login -u [Dockerhubusername]
Eg: $ docker login -u sowjanyajindam

o	$ docker tag imagename Dockerhubusername/imagename Eg: $ docker tag calciimage sowjanyajindam/calciimage

o	$ docker push Dockerhubusername/imagename Eg: $ docker push sowjanyajindam/calciimage

	Pull the code from Docker hub and execute
o	$  docker pull sowjanyajindam/calciimage
o	$ docker run -it sowjanyajindam/calciimage

EXPERIMENT NO. 15

AIM: Containerization of an application.
Case Study #2: Develop a Application (MINI-Project) Dockerize the program and push the containerized application code to GitHub and DockerHub.

1.	Abstract of you Mini Project.
2.	Code.
3.	Execution steps.
4.	GITHUB URL.
5.	DOCKERHUB URL.


