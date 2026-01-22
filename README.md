# spring3-jenkins-pipeline-practice

This repository is created for **learning and practicing Jenkins CI pipelines with a Maven project**.

The project is intentionally simple so you can clearly understand:

* Maven project structure
* Jenkins pipeline execution
* GitHub → Jenkins integration

---

## 📌 Project Overview

This is a **basic Java Maven project** that:

* Compiles Java source code using Maven
* Runs through a Jenkins pipeline
* Produces a JAR file

It is suitable for:

* Jenkins beginners
* CI/CD practice
* Interview preparation

---

## 📁 Project Structure

```
spring3-jenkins-pipeline-practice/
├── pom.xml
├── Jenkinsfile
└── src/
    └── main/
        └── java/
            └── com/
                └── example/
                    └── App.java
```

---

## 📄 pom.xml (Maven Configuration)

The `pom.xml` file is the **heart of a Maven project**. It defines:

* Project details
* Java version
* Plugins used during build

### 🔑 Key Configuration

* Java version: **1.8**
* Maven Compiler Plugin: **3.10.1**

### Why Maven Compiler Plugin?

Jenkins often fails builds when:

* Java version is not defined
* Old compiler plugins are used

So we explicitly configure it:

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.10.1</version>
    <configuration>
        <source>1.8</source>
        <target>1.8</target>
    </configuration>
</plugin>
```

---

## 📄 App.java (Sample Java Code)

Location:

```
src/main/java/com/example/App.java
```

Purpose:

* Simple Java class to verify Maven compilation
* Prints a success message

```java
package com.example;

public class App {
    public static void main(String[] args) {
        System.out.println("Jenkins Maven Build Successful!");
    }
}
```

---

## 📄 Jenkinsfile (CI Pipeline)

The `Jenkinsfile` defines the **CI pipeline as code**.

### Pipeline Stages

1. **Checkout** – Pulls code from GitHub
2. **Build** – Runs Maven build

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}
```

---

## ⚙️ Prerequisites

Before running Jenkins pipeline, ensure:

### On Jenkins Server

* Java 8 or above installed
* Maven installed
* Git installed

Check versions:

```bash
java -version
mvn -version
git --version
```

---

## 🔗 GitHub Repository Setup

### 1️⃣ Create Repository

```text
Repository name: spring3-jenkins-pipeline-practice
Visibility: Public
```

### 2️⃣ Upload Files

You can upload using **GitHub UI**:

* Add `pom.xml`
* Add `Jenkinsfile`
* Add `src/` folder

Or using Git CLI:

```bash
git init
git branch -M main
git remote add origin https://github.com/gayas5/spring3-jenkins-pipeline-practice.git
git add .
git commit -m "Initial Maven project"
git push -u origin main
```

---

## 🚀 Jenkins Pipeline Setup

### Step 1: Create Jenkins Job

* New Item → **Pipeline**
* Job name: `maven-ci-pipeline`

### Step 2: Configure Pipeline

* Definition: **Pipeline script from SCM**
* SCM: **Git**
* Repository URL:

  ```
  https://github.com/gayas5/spring3-jenkins-pipeline-practice.git
  ```
* Branch:

  ```
  */main
  ```

Save the job.

---

## ▶️ Run the Build

Click **Build Now** in Jenkins.

### Expected Output

```text
[INFO] BUILD SUCCESS
```

A JAR file will be generated at:

```
target/spring3-jenkins-pipeline-practice-1.0-SNAPSHOT.jar
```

---

## ❌ Common Errors & Fixes

### Maven not found

```text
mvn: command not found
```

Fix:

* Install Maven on Jenkins server
* Configure Maven in Jenkins → Global Tool Configuration

---

### Java version error

Fix:

* Ensure Java 8+ installed
* Verify `maven-compiler-plugin` configuration

---

## 🎯 Next Improvements

You can extend this project by adding:

* Spring MVC / Spring Boot
* Dockerfile
* Docker image build in Jenkins
* Deployment to Kubernetes
* ArgoCD integration

---

## 👤 Author

**Md Gayasuddin**

---

✅ This repository is created purely for **learning Jenkins CI pipelines with Maven**.
