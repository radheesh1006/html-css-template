pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/radheesh1006/html-css-template.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t myapp-image .'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                bat '''
                docker stop myapp-container || echo "No container running"
                docker rm myapp-container || echo "No container to remove"
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 80:80 --name myapp-container myapp-image'
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
