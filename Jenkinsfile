pipeline {
    agent any

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
                // Add build steps here
                // Example: sh 'mvn clean install'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Add test steps here
                // Example: sh 'mvn test'
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

        stage('Code Analysis') {
            steps {
                echo 'Conducting Code Quality Analysis...'
                // Add code analysis steps here
                // Example: sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Executing Security Scan...'
                // Add security scan steps here
                // Example: sh 'snyk test'
            }
            post {
                always {
                    script {
                        def log = currentBuild.rawBuild.getLog(50).join('\n') // Gets the last 50 lines of the log
                        mail to: "cketipearachchi@gmail.com",
                            subject: "Security Scan - ${currentBuild.currentResult}",
                            body: "Security Scan completed with status: ${currentBuild.currentResult}\n\nHere are the last 50 lines of the log:\n${log}"
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying Application to Staging Environment...'
                // Add deployment steps here
                // Example: sh 'scp target/app.jar user@staging-server:/deploy-path'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Performing Integration Tests on Staging Environment...'
                // Add integration test steps here
                // Example: sh 'mvn verify -P integration-test'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying Application to Production Environment...'
                // Add production deployment steps here
                // Example: sh 'aws s3 cp app.war s3://mybucket/app.war'.
            }
        }
    }
}
