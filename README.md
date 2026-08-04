     EXPERIMENT NO. 1
AIM: Write code for a simple user registration form for an event. Program:
registration.html

<html>
<head>
<link href="register.css" rel="stylesheet" />
</head>

<body>
<h1> DevOps Lab</h1>

<h2> Student Registration Form</h1>
<form>
<table border="5" align="center" cellspacing="10" cellpadding="10" >

<tr>
<td>Name</td><td><input type="text"></td>
</tr>

<tr>
<td>Contact Number</td>
<td><input type="text"></td>
</tr>

<tr>
<td>Gender</td>
<td><input type="radio" name="g">Male
<input type="radio" name="g">Female</td>
</tr>

<tr>
<td>Address</td>
<td><textarea rows="5" cols="15"></textarea></td>
</tr>

<tr>
<td>Hobbies</td>
<td><input type="checkbox">Singing
<input type="checkbox">Travelling
<input type="checkbox">Reading novels
</td>
</tr>
<tr>
<td>Skillset</td>
<td><input type="checkbox">C
<input type="checkbox">Python
<input type="checkbox">Java
</td>
</tr>

<tr>
<td>Highest Qualification</td>
<td><select>
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
<td><select>
<option>--SELECT--></option>
<option>Adilabad</option>
<option>Zaheerabad</option>
</select>
</td>
</tr>

<tr>
<td><input type="submit" value="Register"></td>
<td><input type="reset" value="Clear"></td>
</tr>


</table>
</body>
</html>

register.css


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

Output:






EXPERIMENT NO. 2
Program: GitHub Commands for Pushing the data from local repository to remote github repository

Step 1: Sign in to your GitHub account.
Step 2: Create a Repository

•	Click on Create a new repository
•	Create a Public Repository by name samplerepo
•	Copy the git url

Step 3: Check version & Configure the settings
•	$ git --version
•	$ git config --global user.name “sowjanya”
•	$ git config --global user.email “sowjanya@gmail.com”
•	$ git remote add origin https://github.com/sowjanya/samplerepo.git
•	$ git config --list
Step 4: Create directory & initialize it
•	$ mkdir demo
•	$ cd demo
•	$ git init

Step 5: Create new file, see status, put in staging area & commit into local repo
•	$ touch myfile.txt
•	$ vi myfile.txt (put some content)
•	$ git status
•	$ git add .
•	$ git commit -m "1st commit file added"
•	$ git log
•	$ git show <commit-id>
•	$ git status
•	$ git branch -M main
•	$ git push -u origin main
Step 6: Go to remote repository and check whether project is uploaded on github.
EXPERIMENT NO. 3
Local repository to Remote Repository:
Step 1: Create directory

$ mkdir studregistration
$ cd studregistration
$ git init
Step 2: Create new repository in your GitHub account and copy URL

Step 3: Configure your user details and Set URL
$ git remote add origin <centralgit repo url>
$ git config --global user.name “username”
$ git config --global user.email “user@mail.com”
$ git config --list


Step 4: Create new files and add the source code written in exercise 1.

$ vi registration.html
$ vi register.css

Step 5: Check status and add files to git and commit
$ git status
$ git add .
$ git commit –m “Added 2 files”
$ git status
Step 6: Branch to main and push the code
$ git branch –M main
$ git push –u origin main
$ git status
$ git log
                  Step 7: Create a new Branch to main and make changes to file and merge the file.
$ git checkout –b branch1	//creates new branch
$ git branch	// check the branch
$ vi registration.html	//make changes to the content of the file
$ git add .	// add file to git
$ git commit –m “made changes in text file on branch1”
$ git status
$ git push –u origin branch1
$ git status
$ git diff main	// compares main branch and branch1
$ git checkout main
$ git pull origin main
$ git merge branch1
$ git push origin main

EXPERIMENT NO. 4

AIM: Jenkins installation and setup, explore the environment.

Step 1:    
sudo apt update
sudo apt upgrade -y
step 2: Install Java (Jenkins requires Java 11+)
sudo apt install -y openjdk-21-jdk
Verify Java installation:
java -version
You should see something like:
openjdk version "11.0.x" ...

Step 3: Add Jenkins repository and key
Add Jenkins key:
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \ 
https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
 
Step 4: Install Jenkins
sudo apt update
sudo apt install jenkins -y
Step 5: Start and enable Jenkins service
sudo systemctl enable jenkins
sudo systemctl start jenkins





•	$ git add.
•	$ git commit -m “1st commit file added”
•	$ git log
•	$ git show <commit -id>
•	$ git status
•	$ git branch -M main
•	$ git push -u origin main..


Step 6: Go to remote repository and check whether project is uploaded on github.




EXPERIMENT NO. 5


Program #1 : Create a Jenkins Job for executing shell commands

Steps:
•	In browser open https://localhost:8080 and login in using your account.
•	Create a new Jenkins job using the "Freestyle project" type.
o	In the dash board, Click on New item to create job.
o	Assign a meaningful name for the job and select free style project option and click on OK button.
•	Provide a description about application and under Buildsteps option choose execute shell.
•	Type few linux commands in shell window.
o	whoami
o	pwd
o	mkdir demo
o	ls
o	cd demo
o	echo “Hello Jenkins” > sample.txt
o	ls
o	cat sample.txt
•	Cilck on Save button.
•	Click on build now option available in dash board.
•	To watch the output click on Console output

Program #2 : Create a Jenkins Job for executing Java program – Reverse of a number.

Steps:
•	Create a file ReverseNumber.java and type the code for reverse of a number and save file
class ReverseNumber
{
public static void main(String args[])
{
int n=Integer.parseInt(args[0]); int rev=0;
int r; while(n>0)
{
r=n%10;
rev=(rev*10)+r; n=n/10;
}
System.out.println("Reverse number:"+rev);
}
}
•	In browser open https://localhost:8080 and login in using your account.
•	Create a new Jenkins job using the "Freestyle project" type.
•	Provide a description about application and under Buildsteps option choose execute shell.
•	Copy the program into the Jenkins evnvironment workspace.
•	Type commands for execution of your java program.
o	javac ReverseNumber.java
o	java ReverseNumber 1234
•	Cilck on Save button.
•	Click on build now option available in dash board.
•	To watch the output click on Console output


Program #3 : Create a Jenkins Job for executing parameterized Java program – Reverse of a number.

Steps:
•	Create a file PatternDemo.java and type the code for creating pyramid pattern and save file

class PatternDemo
{
    public static void main(String args[])
    {
         int n=Integer.parseInt(args[0]);      for(int i=1;i<=n;i++)
          {
           for(int j=1;j<=i;j++)
             {
                System.out.print(i+"\t");
              }
           System.out.println();
           }
      }
}
•	In browser open https://localhost:8080 and login in using your account.
•	Create a new Jenkins job using the "Freestyle project" type.
o	In the dash board, Click on New item to create job.
o	Assign a meaningful name for the job and select free style project option and click on OK button.
•	In the job configuration, provide description about job and choose "This project is parameterized."
•	Add a "String Parameter" named “n1” and set its default value to 5.
•	Under Buildsteps option choose execute shell.
•	Copy the program into the Jenkins evnvironment workspace.
•	Type commands for execution of your java program.
o	javac PatternDemo.java
o	java PatternDemo $n1
•	Cilck on Save button.
•	Click on build now option available in dash board and it will prompt you to enter value for n1.
•	Enter value for parameter and click ok.
•	To watch the output click on Console output

             Program #4 : Create a Jenkins Job for executing parameterized Java program from the Git repository –     Biggest of three Numbers.

Steps:
•	Create a file Biggest.java and type the code for Biggest of three numbers and save file
class Biggest
{
public static void main(String args[])
{
int n1=Integer.parseInt(args[0]);
int n2=Integer.parseInt(args[1]);
int n3=Integer.parseInt(args[2]);

if((n1>n2)&&(n1>n3))
{
System.out.println(n1+" is biggest");
}
else if((n2>n1)&&(n2>n3))
{
System.out.println(n2+" is biggest");
}
else
{
System.out.println(n3+" is biggest");
}
}
}
•	Login into your GitHub Account and create a new repository with name “Biggestnum”
•	Upload the file Biggest.java into your GitHub repository and commit the changes.
•	Copy the URL of your Git Repository
•	In browser open https://localhost:8080 and login in using your account.
•	Create a new Jenkins job using the "Freestyle project" type.
o	In the dash board, Click on New item to create job.
o	Assign a meaningful name for the job and select free style project option and click on OK button.
•	In the job configuration, provide description about job and choose "This project is parameterized."Add 3 "String Parameter" named “n1” , “n2” nad “n3” and set its default values.
•	Under source management choose Git and provide the Git URL there.
•	Set Branches to build -> Branch Specifier to the working Git branch (ex */main)
•	Under Buildsteps option, choose execute shell.
•	Type commands for execution of your java program.
o	javac Biggest.java
o	java Biggest $n1 $n2 $n3
•	Cilck on Save button.
•	Click on build parameterized now option available in dash board and it will prompt you to enter value for n1, n2 ad n3.
•	Enter values for parameter and click ok.
•	To watch the output click on Console output.
Program #5 : Create a Jenkins pipeline Job using pipeline script.

Steps:
•	In browser open https://localhost:8080 and login in using your account.
•	Create a new Jenkins job using the "pipeline" project type.
o	In the dash board, Click on New item to create job.
o	Assign a meaningful name for the job and select pipeline project option and click on OK button.
•	In the job configuration, provide description about job.
•	Type the following script under the space provided for writing the script.
pipeline { agent any stages{
stage('compile'){ steps{
echo "Compiled Successfully";
}
}
stage('Junit'){ steps{
echo "JUnit test passed Successfully";
}
}
stage('Qualitycheck'){ steps{
echo " Quality Check passed Successfully";
}
}
stage('Deploy'){ steps{
echo "Deployed Successfully";
}
}

}

post{
always{
cho "This will always run"
}
success{
echo "This will run on success"
}
failure{
echo "This will run on failure"
}
unstable{
echo "This will run only if the run is marked as Unstable"
}
changed{
echo "Pipe line changed"
}
}
}

•	Cilck on Save button.
•	Click on build now option available in dash board.
•	To watch the output click on Console out

