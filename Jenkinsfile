pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_USERNAME/flask-jenkins-deploy.git'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    // Building a Docker image
                    sh 'docker build -t flask-app-image .'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Remove old container if it exists
                    sh 'docker stop flask-container || true'
                    sh 'docker rm flask-container || true'
                    
                    // Run the new container
                    sh 'docker run -d -p 5000:5000 --name flask-container flask-app-image'
                }
            }
        }
    }
}
