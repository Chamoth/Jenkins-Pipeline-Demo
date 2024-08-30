pipeline {
    agent any

    stages {
        stage('Wait for Short Delay') {
            steps {
                script {
                    echo 'Pausing for 10 seconds before pipeline starts...'
                    sleep time: 10, unit: 'SECONDS'  // Adjust the delay as necessary
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Initiating Build Process'
                // Use a build tool such as Maven or Gradle for project compilation
                // Example: sh 'mvn clean install'
                // Example: sh './gradlew build'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Execute tests using tools like JUnit, TestNG, or NUnit
                // Example: sh 'mvn test'
                // Example: sh './gradlew test'
                // Example: sh 'dotnet test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Conducting Code Quality Analysis...'
                // Perform code analysis with tools such as SonarQube, Checkstyle, or PMD
                // Example: sh 'mvn sonar:sonar'
                // Example: sh './gradlew sonarqube'
                // Example: sh 'mvn checkstyle:check'
                // Example: sh 'mvn pmd:check'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Executing Security Scan...'
                // Run security scans with tools like OWASP ZAP, Snyk, or Bandit
                // Example: sh 'zap-cli quick-scan http://localhost:8080'
                // Example: sh 'snyk test'
                // Example: sh 'bandit -r /path/to/code'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying Application to Staging Environment...'
                // Deploy to a staging server using methods like AWS EC2, Docker, or Kubernetes
                // Example: sh 'scp target/app.jar user@staging-server:/deploy-path'
                // Example: sh 'docker build -t myapp:latest . && docker run -d -p 8080:8080 myapp:latest'
                // Example: sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Performing Integration Tests on Staging Environment...'
                // Run integration tests on staging using tools like Selenium, Cucumber, or Postman
                // Example: sh 'ssh user@staging-server "java -jar /deploy-path/app.jar && run-integration-tests.sh"'
                // Example: sh 'mvn verify -P integration-test'
                // Example: sh 'newman run collection.json'
                // Example: sh 'cucumber -f pretty -f json:report.json'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying Application to Production Environment...'
                // Deploy your application to production using methods such as AWS EC2, Docker, or Kubernetes
                // Example: sh 'aws s3 cp app.war s3://mybucket/app.war'
                // Example: sh 'docker-compose -f docker-compose.prod.yml up -d'
                // Example: sh 'kubectl rollout update deployment myapp-deployment'
            }
        }
    }

    post {
        success {
            script {
                def log = currentBuild.rawBuild.getLog(50).join('\n') // Retrieves the last 50 lines of the build log
                mail to: "cketipearachchi@gmail.com",
                     subject: "Build Status Notification - Success",
                     body: "The build was successful! Please review the details below.\n\nHere are the last 50 lines of the build log:\n${log}"
            }
        }
        failure {
            script {
                def log = currentBuild.rawBuild.getLog(50).join('\n') // Retrieves the last 50 lines of the build log
                mail to: "cketipearachchi@gmail.com",
                     subject: "Build Status Notification - Failure",
                     body: "The build failed. Check the logs for further details.\n\nHere are the last 50 lines of the build log:\n${log}"
            }
        }
    }
}
