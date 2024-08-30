pipeline {
    agent any

    stages {
        stage('Wait for Short Delay') {
            steps {
                script {
                    echo 'Waiting for 10 seconds before starting the pipeline...'
                    sleep time: 10, unit: 'SECONDS'  // Adjust the delay as needed
                }
            }
        }


        stage('Build') {
            steps {
                echo 'Starting Build Stage'
                // Use a build tool like Maven or Gradle to build the project
                // Example: sh 'mvn clean install'
                // Example: sh './gradlew build'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Executing Unit and Integration Tests...'
                // Use a test automation tool like JUnit, TestNG, or NUnit for tests
                // Example: sh 'mvn test'
                // Example: sh './gradlew test'
                // Example: sh 'dotnet test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                // Use a tool like SonarQube, Checkstyle, or PMD for code analysis
                // Example: sh 'mvn sonar:sonar'
                // Example: sh './gradlew sonarqube'
                // Example: sh 'mvn checkstyle:check'
                // Example: sh 'mvn pmd:check'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Conducting Security Scan...'
                // Use a security scanning tool like OWASP ZAP, Snyk, or Bandit for security scanning
                // Example: sh 'zap-cli quick-scan http://localhost:8080'
                // Example: sh 'snyk test'
                // Example: sh 'bandit -r /path/to/code'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying Application to Staging Environment...'
                // Deploy to a cloud server like AWS EC2, Docker, or Kubernetes
                // Example: sh 'scp target/app.jar user@staging-server:/deploy-path'
                // Example: sh 'docker build -t myapp:latest . && docker run -d -p 8080:8080 myapp:latest'
                // Example: sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging Environment...'
                // Run tests on staging server using tools like Selenium, Cucumber, or Postman
                // Example: sh 'ssh user@staging-server "java -jar /deploy-path/app.jar && run-integration-tests.sh"'
                // Example: sh 'mvn verify -P integration-test'
                // Example: sh 'newman run collection.json'
                // Example: sh 'cucumber -f pretty -f json:report.json'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying Application to Production Environment...'
                // Deploy your application to a production server (e.g., AWS EC2, Docker, or Kubernetes)
                // Example: sh 'aws s3 cp app.war s3://mybucket/app.war'
                // Example: sh 'docker-compose -f docker-compose.prod.yml up -d'
                // Example: sh 'kubectl rollout update deployment myapp-deployment'
            }
        }
    }

    post {
        success {
            script {
            def log = currentBuild.rawBuild.getLog(50).join('\n') // Gets the last 50 lines of the log
            mail to: "cketipearachchi@gmail.com",
                 subject: "Build Status Email - Success",
                 body: "Build was successful! Changes are made here \n\nHere are the last 50 lines of the log:\n${log}"
            }
        }
        failure {
            script {
                def log = currentBuild.rawBuild.getLog(50).join('\n') // Gets the last 50 lines of the log
                mail to: "cketipearachchi@gmail.com",
                     subject: "Build Status Email - Failure",
                     body: "Build failed. Please check the logs for more details.\n\nHere are the last 50 lines of the log:\n${log}"
            }
        }
    }
}
