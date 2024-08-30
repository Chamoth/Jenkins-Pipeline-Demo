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
                script {
                    echo 'Building the application...'
                    // Use Maven to build the project
                    sh 'mvn clean package'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Run unit and integration tests using Maven
                    sh 'mvn test'
                }
            }
            post {
                always {
                    // Collect test results
                    junit 'target/surefire-reports/*.xml'
                    // Send email notification after tests
                    emailext(
                        subject: "Jenkins Pipeline: Unit/Integration Tests",
                        body: "The Unit and Integration tests have completed. Check the attached results.",
                        to: "dev-team@example.com",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing code...'
                    // Perform code analysis using SonarQube
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Perform security scan using OWASP Dependency-Check or Snyk
                    sh 'mvn dependency-check:check'
                }
            }
            post {
                always {
                    // Send email notification after security scan
                    emailext(
                        subject: "Jenkins Pipeline: Security Scan",
                        body: "The Security Scan has completed. Check the attached results.",
                        to: "dev-team@example.com",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging environment...'
                    // Deploy the application to a staging server (example: AWS EC2)
                    sh 'scp target/myapp.war user@staging-server:/path/to/deploy'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging environment...'
                    // Run integration tests on the staging environment
                    sh 'curl -X GET http://staging-server/api/test'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production environment...'
                    // Deploy the application to the production server
                    sh 'scp target/myapp.war user@production-server:/path/to/deploy'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
            // Optionally send a success notification
            emailext(
                subject: "Jenkins Pipeline: Success",
                body: "The Jenkins pipeline completed successfully.",
                to: "dev-team@example.com"
            )
        }
        failure {
            echo 'Pipeline failed!'
            // Send a failure notification
            emailext(
                subject: "Jenkins Pipeline: Failure",
                body: "The Jenkins pipeline failed. Please check the logs for more details.",
                to: "dev-team@example.com",
                attachLog: true
            )
        }
    }
}
