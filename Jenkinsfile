pipeline {
    agent any

    environment {
        EMAIL_RECIPIENTS = 'cketipearachchi@gmail.com'
        EMAIL_SUBJECT = "Jenkins Pipeline Notification"
    }

    stages {
        stage('Wait for Short Delay') {
            steps {
                script {
                    echo 'Pausing for 10 seconds before pipeline starts...'
                    sleep time: 10, unit: 'SECONDS'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Initiating Build Process'
                // Add your build steps here
                // Example: sh 'mvn clean install'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Add your test steps here
                // Example: sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Conducting Code Quality Analysis...'
                // Add your code analysis steps here
                // Example: sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Executing Security Scan...'
                // Add your security scan steps here
                // Example: sh 'snyk test'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying Application to Staging Environment...'
                // Add your deployment steps here
                // Example: sh 'scp target/app.jar user@staging-server:/deploy-path'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Performing Integration Tests on Staging Environment...'
                // Add your integration test steps here
                // Example: sh 'mvn verify -P integration-test'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying Application to Production Environment...'
                // Add your production deployment steps here
                // Example: sh 'aws s3 cp app.war s3://mybucket/app.war'
            }
        }
    }

    post {
        always {
            script {
                def log = currentBuild.rawBuild.getLog(50).join('\n') // Retrieves the last 50 lines of the build log
                def status = currentBuild.currentResult
                def subject = "Build Status Notification - ${status}"

                emailext (
                    to: "${EMAIL_RECIPIENTS}",
                    subject: subject,
                    body: """
                    The build ${status} at ${env.BUILD_URL}.

                    Here are the last 50 lines of the build log:

                    ${log}
                    """,
                    attachmentsPattern: "**/build.log", // Adjust the path to your actual log file if necessary
                    compress: true
                )
            }
        }
    }
}
