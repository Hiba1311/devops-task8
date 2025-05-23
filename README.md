 TASK 8:
 Run a Simple Java Maven Build Job in Jenkins

OBJECTIVE:
Learn how to use Jenkins to build a simple Java application using Maven — your first step into CI/CD.

 TOOLS REQUIRED:
•	Jenkins (installed locally or via Docker)
•	Java JDK 8 or 11
•	Maven
•	Git (optional — can run from local folder)
•	VS Code (for editing files)
•	Docker Desktop

 PROJECT NAME:
hello-java

DELIVERABLES:
•	A basic Java HelloWorld app (with pom.xml)
•	Jenkins Freestyle job configured to build it
•	Screenshot of successful build console output

 Java + Maven + Jenkins CI/CD Setup Guide

This guide will walk you through setting up a simple Java Maven project and building it with Jenkins using Docker.  

Your working directory is: `C:\Devops-internship\task8`

Part 1: Create Java Maven Project in VS Code

Step 1: Open VS Code in your project folder
powershell
cd "C:\Devops-internship\task8"
code .

Step 2: Create Folder Structure
Inside VS Code:
 Create folders: src/main/java

 Step 3: Create HelloWorld.java inside src/main/java

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Jenkins + Maven!");
    }
}

Step 4: Create `pom.xml` in the root folder

<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>hello</artifactId>
  <version>1.0</version>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>

Part 2: Run Jenkins with Docker

Step 1: Run Jenkins Container

docker run -d --name jenkins-container -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

Step 2: Unlock Jenkins

docker exec jenkins-container cat /var/jenkins_home/secrets/initialAdminPassword

- Paste the password into the Jenkins UI (`http://localhost:8080`)
- Install Suggested Plugins and create admin user if prompted

 Part 3: Setup JDK and Maven in Jenkins

- Go to: Manage Jenkins → Global Tool Configuration
- Under JDK:
  - Add JDK: Name = JDK11, check Install automatically
- Under Maven:
  - Add Maven: Name = Maven 3.8.6, check Install automatically

 Part 4: Create Jenkins Job

 Step 1: Create Freestyle Project
- Name: hello-java
- Type: Freestyle

Step 2: Copy Project into Jenkins Container

docker cp "C:\Devops-internship\trial and error 8" jenkins-container:/var/jenkins_home/workspace/hello-java-job

Step 3: Configure Build Step
- In Build → Add build step → Invoke top-level Maven targets
- Goals: clean package



Part 5: Run & Verify Build

- In Jenkins: open `hello-java-job` → Click Build Now
- Click build number → Console Output

You should see:
[INFO] BUILD SUCCESS

 You're done! Your Maven build is working through Jenkins and Docker.

Hiba Siddiqui
