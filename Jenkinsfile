pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the application...'
                    // Use Maven as the build automation tool
                    sh 'mvn clean package'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Use JUnit for unit testing and integration testing
                    sh 'mvn test'
                }
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' // Collect test results
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing code...'
                    // Use SonarQube for static code analysis
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Use OWASP Dependency-Check or Snyk for security scanning
                    sh 'mvn dependency-check:check'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging environment...'
                    // Example: Deploy to an AWS EC2 instance using SSH
                    sh 'scp target/myapp.war user@staging-server:/path/to/deploy'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging environment...'
                    // Example: Use Postman or another tool to test the staging environment
                    sh 'curl -X GET http://staging-server/api/test'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production environment...'
                    // Example: Deploy to an AWS EC2 instance using SSH
                    sh 'scp target/myapp.war user@production-server:/path/to/deploy'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
            // Example: Send email notification on success
            mail to: 'dev-team@example.com',
                 subject: 'Pipeline Success',
                 body: "The pipeline has completed successfully."
        }
        failure {
            echo 'Pipeline failed!'
            // Example: Send email notification on failure
            mail to: 'dev-team@example.com',
                 subject: 'Pipeline Failure',
                 body: "The pipeline has failed. Please check the logs for details."
        }
    }
}
