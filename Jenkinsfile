pipeline {
    agent any

    environment {
        DIRECTORY_PATH = '/path/to/your/code'
        TESTING_ENVIRONMENT = 'staging'
        PRODUCTION_ENVIRONMENT = 'YourName-Production'
        RECIPIENTS = 'henryxie666888@gmail.com' // Add your email here
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
                // Simulating test logs
                sh 'echo "Unit and Integration test logs" > test.log'
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Checking the quality of the code"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the application to a testing environment specified by the environment variable: ${env.TESTING_ENVIRONMENT}"
                // Simulating deployment logs
                sh 'echo "Deployment logs" > deploy.log'
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
            echo "Pipeline executed successfully. Sending email with logs."
            emailext(
                to: "${env.RECIPIENTS}",
                subject: "Pipeline ${currentBuild.fullDisplayName} succeeded",
                body: "Good news! The pipeline has succeeded. Logs are attached.",
                attachLog: true,
                attachmentsPattern: '**/*.log' // Attaching the log files
            )
        }
        failure {
            echo "Pipeline failed. Sending failure email."
            emailext(
                to: "${env.RECIPIENTS}",
                subject: "Pipeline ${currentBuild.fullDisplayName} failed",
                body: "Unfortunately, the pipeline has failed. Please check the logs attached.",
                attachLog: true,
                attachmentsPattern: '**/*.log' // Attaching the log files
            )
        }
        always {
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
            echo "Archiving logs"
        }
    }
}
