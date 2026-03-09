# 🚀 Jenkins CI Pipeline with SonarQube and Nexus Artifact Repository

---

# 📌 Project Overview

This project demonstrates a **complete Continuous Integration (CI) pipeline** using **GitHub, Jenkins, SonarQube, Maven, and Nexus Repository**.

The application used in this pipeline is a **Spring Boot Employee API built with Maven**.

Whenever a developer pushes code to the GitHub repository, a **GitHub Webhook automatically triggers the Jenkins pipeline**.

The pipeline performs the following tasks:

* Jenkins automatically pulls the latest source code from the GitHub repository
* Maven builds the application and runs automated tests
* SonarQube scans the code to detect bugs, vulnerabilities, and code quality issues
* Quality Gate verifies whether the code meets the required quality standards
* Maven packages the application into a deployable JAR artifact
* The final artifact is deployed and stored in **Nexus Repository** for future deployments

This architecture ensures that **only tested and quality-approved artifacts are stored in a centralized Nexus repository before deployment**.

---

# 🧭 CI Pipeline Architecture

The following diagram represents the CI pipeline implemented in this project.

```
Developer Push Code
        │
        ▼
GitHub Repository
        │
        ▼
GitHub Webhook Trigger
        │
        ▼
Jenkins Pipeline
        │
        ├── Checkout Code
        ├── Build (Maven)
        ├── Run Tests
        ├── SonarQube Code Analysis
        │
        ▼
Quality Gate Check
        │
        ├── ❌ Failed → Pipeline Stops
        │
        └── ✅ Passed → Continue Pipeline
                        │
                        ▼
                 Package Artifact (JAR)
                        │
                        ▼
              Deploy Artifact to Nexus
```

---

# ⚙️ Tech Stack

* Java 17
* Spring Boot
* Maven
* Jenkins
* SonarQube
* Nexus Repository Manager
* Git
* GitHub
* GitHub Webhooks

---

# 📂 Project Structure

```
jenkins-sonarqube-nexus-ci
│
├── Jenkinsfile
├── pom.xml
├── README.md
├── settings.xml
└── src
     └── main
          ├── java/com/example/employee
          │     ├── EmployeeApiApplication.java
          │     └── HelloController.java
          │
          └── resources
                └── application.properties
```

---

# ⚙️ Jenkins Pipeline Stages

The Jenkins pipeline is implemented using a **Jenkinsfile** and consists of the following stages.

---

## 1️⃣ Checkout

Jenkins pulls the latest source code from the **GitHub repository**.

---

## 2️⃣ Build

```
mvn compile
```

Maven compiles the application source code.

---

## 3️⃣ Test

```
mvn test
```

Runs automated unit tests to verify application functionality.

---

## 4️⃣ SonarQube Code Analysis

```
mvn sonar:sonar
```

Performs static code analysis using SonarQube and checks for:

* Bugs
* Vulnerabilities
* Code Smells
* Security issues

---

## 5️⃣ Quality Gate Validation

After analysis, SonarQube sends the result to Jenkins using a **SonarQube Webhook**.

Jenkins waits for the Quality Gate result.

* If the Quality Gate **fails**, the pipeline stops.
* If the Quality Gate **passes**, the pipeline continues.

---

## 6️⃣ Package Application

```
mvn package
```

This generates the final artifact:

```
target/employee-api-1.0.0.jar
```

---

## 7️⃣ Deploy Artifact to Nexus Repository

The pipeline includes a **deploy stage** that uploads the generated artifact to **Nexus Repository Manager**.

```
mvn deploy
```

The artifact is stored and versioned in Nexus so it can later be used for deployment.

---

# ⚙️ Maven Configuration for Nexus Deployment

## 🔹 pom.xml Configuration

```
<distributionManagement>
  <repository>
    <id>nexus</id>
    <url>http://NEXUS-IP:8081/repository/maven-releases/</url>
  </repository>
</distributionManagement>
```

---

## 🔹 settings.xml Configuration

Location:

```
~/.m2/settings.xml
```

Configuration:

```
<servers>
  <server>
    <id>nexus</id>
    <username>admin</username>
    <password>password</password>
  </server>
</servers>
```

This allows Maven to authenticate with Nexus during deployment.

---

# 🔄 CI Pipeline Workflow

```
Developer Push Code → GitHub
            ↓
GitHub Webhook Trigger
            ↓
Jenkins Pipeline
            ↓
Build + Test
            ↓
SonarQube Code Analysis
            ↓
Quality Gate Validation
            ↓
Package Artifact
            ↓
Deploy Artifact to Nexus Repository
```

---

# 📸 Project Screenshots

### Jenkins Pipeline Execution

![Jenkins Pipeline](Screenshot/jenkins-pipeline.png)

---

### SonarQube Analysis Dashboard

![SonarQube Dashboard](Screenshot/sonarqube-dashboard.png)

---

### Nexus Artifact Repository

![Nexus Repository](Screenshot/nexus-artifact.png)

---

### GitHub Webhook Configuration

![GitHub Webhook](Screenshot/github-webhook.png)

---

# 📦 Artifact Stored in Nexus

After successful pipeline execution, the artifact is uploaded to Nexus.

Example artifact:

```
employee-api-1.0.0.jar
```

Benefits of Nexus:

* Centralized artifact storage
* Artifact version management
* Reliable deployments
* Artifact reuse in CD pipelines

---

# 🎯 What This Project Demonstrates

* Jenkins CI pipeline creation
* GitHub Webhook automation
* SonarQube integration with Jenkins
* Quality Gate validation
* Maven build lifecycle
* Artifact management using Nexus
* Automated CI pipeline for build, testing, analysis, and artifact deployment

---

# 💼 Why This Project Matters

In real DevOps environments, build artifacts are stored in **artifact repositories like Nexus** instead of being directly deployed.

This ensures:

* artifact version tracking
* centralized storage
* reliable deployments
* separation between CI and CD pipelines

This project demonstrates a **real-world CI pipeline architecture used in many DevOps environments**.

---

# 👨‍💻 Author

Developed as part of hands-on practice to strengthen **AWS, DevOps, CI/CD pipelines, artifact management, and automation skills**.
