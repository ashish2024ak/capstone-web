pipeline {
    agent any

    stages {
        stage('Pull from GitHub') {
            steps {
                echo 'GitHub repository already cloned.'
            }
        }

        stage('Deploy to AWS') {
            steps {
                sh 'sudo cp indexaws.html /var/www/html/index.html'
                sh 'sudo systemctl restart nginx'
            }
        }

        stage('Deploy to Azure') {
            steps {
                sh 'scp -i ~/azure-key indexazure.html azureuser@52.190.23.107:/var/www/html/index.html'
                sh 'ssh -i ~/azure-key azureuser@52.190.23.107 "sudo systemctl restart nginx"'
            }
        }
    }
}

