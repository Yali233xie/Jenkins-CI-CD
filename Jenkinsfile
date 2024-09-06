pipeline {
    agent any

    environment {
        DIRECTORY_PATH = '/path/to/your/code'
        TESTING_ENVIRONMENT = 'staging'
        PRODUCTION_ENVIRONMENT = 'YourName-Production'
        RECIPIENTS = 'henryxie666888@gmail.com'  // 你的邮箱地址
    }

    stages {
        stage('Build') {
            steps {
                echo "从指定目录路径获取源代码：${env.DIRECTORY_PATH}"
                echo "编译代码并生成必要的构建产物"
            }
        }
        stage('Test') {
            steps {
                echo "运行单元测试"
                echo "运行集成测试"
                // 假设生成了一个测试日志文件
                sh 'echo "Test logs" > test.log'
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "检查代码质量"
            }
        }
        stage('Security Scan') {
            steps {
                echo "运行安全扫描"
                // 假设生成了一个安全扫描日志文件
                sh 'echo "Security scan logs" > security_scan.log'
            }
        }
        stage('Deploy') {
            steps {
                echo "将应用程序部署到测试环境：${env.TESTING_ENVIRONMENT}"
            }
        }
        stage('Approval') {
            steps {
                echo "等待手动批准"
                sleep time: 10, unit: 'SECONDS'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "将代码部署到生产环境：${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }

    post {
        always {
            // 归档日志文件
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
        }

        success {
            // 在测试和安全扫描阶段后发送邮件通知
            emailext(
                to: "${env.RECIPIENTS}",
                subject: "流水线 ${env.JOB_NAME} #${env.BUILD_NUMBER} 成功",
                body: "好消息！流水线已成功完成。请查看附件中的日志文件。",
                attachmentsPattern: '**/*.log',
                attachLog: true
            )
        }

        failure {
            emailext(
                to: "${env.RECIPIENTS}",
                subject: "流水线 ${env.JOB_NAME} #${env.BUILD_NUMBER} 失败",
                body: "很遗憾，流水线失败了。请查看附件中的日志文件以获取更多信息。",
                attachmentsPattern: '**/*.log',
                attachLog: true
            )
        }
    }
}
