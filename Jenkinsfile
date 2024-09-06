pipeline {
    agent any

    environment {
        DIRECTORY_PATH = '/path/to/your/code'
        TESTING_ENVIRONMENT = 'staging'
        PRODUCTION_ENVIRONMENT = 'YourName-Production'
        RECIPIENTS = 'henryxie666888@gmail.com'  // Add your email here
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artifacts"
            }
        }
        stage('Test') {
            steps {
                echo "Running unit tests"
                echo "Running integration tests"
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Checking the quality of the code"
            }
        }
        stage('Security Scan') {
            steps {
                echo "Running security scans"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the application to a testing environment specified by the environment variable: ${env.TESTING_ENVIRONMENT}"
            }
        }
        stage('Approval') {
            steps {
                echo "Waiting for manual approval"
                sleep time: 10, unit: 'SECONDS'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }

    post {
        success {
            mail to: "${env.RECIPIENTS}",
                subject: "Pipeline ${currentBuild.fullDisplayName} succeeded",
                body: "Good news! The pipeline has succeeded. Logs are attached.",
                attachmentsPattern: '**/*.log' // Modify this pattern based on the log file format
        }
        failure {
            mail to: "${env.RECIPIENTS}",
                subject: "Pipeline ${currentBuild.fullDisplayName} failed",
                body: "Unfortunately, the pipeline has failed. Please check the Jenkins job for more details. Logs are attached.",
                attachmentsPattern: '**/*.log' // Modify this pattern based on the log file format
        }
        always {
            echo "Pipeline execution complete."
        }
    }
}
