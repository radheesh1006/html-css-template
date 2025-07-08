pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                  git branch: 'main', url: 'https://github.com/radheesh1006/html-css-template.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t html-template-image .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker stop html-template-container || echo "No container to stop"
                docker rm html-template-container || echo "No container to remove"
                docker run -d -p 80:80 --name html-template-container html-template-image
                '''
            }
        }
    }
}
