pipeline {
    agent any

    environment {
        GIT_REPO   = 'https://github.com/ashish2024ak/capstone-web.git'
        AWS_USER   = 'ubuntu'
        AWS_IP     = 'YOUR_AWS_PUBLIC_IP'
        AZURE_USER = 'azureuser'
        AZURE_IP   = 'YOUR_AZURE_PUBLIC_IP'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git "${GIT_REPO}"
            }
        }

        stage('Deploy to AWS') {
            steps {
                sh """
                scp -o StrictHostKeyChecking=no index-aws.html ${AWS_USER}@${AWS_IP}:/tmp/index.html
                ssh -o StrictHostKeyChecking=no ${AWS_USER}@${AWS_IP} 'sudo mv /tmp/index.html /var/www/html/index.html && sudo systemctl restart nginx'
                """
            }
        }

        stage('Deploy to Azure') {
            steps {
                sh """
                scp -o StrictHostKeyChecking=no index-azure.html ${AZURE_USER}@${AZURE_IP}:/tmp/index.html
                ssh -o StrictHostKeyChecking=no ${AZURE_USER}@${AZURE_IP} 'sudo mv /tmp/index.html /var/www/html/index.html && sudo systemctl restart nginx'
                """
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}

