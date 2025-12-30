pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // 'checkout scm' automatically uses the repo you configured in the Jenkins UI
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                script {
                    // Use 'bat' instead of 'sh' because you are on Windows
                    bat 'docker build -t flask-app-image .'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Use 'bat' for Windows. These commands stop and clean up old containers
                    // The "|| exit 0" ensures the pipeline doesn't fail if the container doesn't exist yet
                    bat 'docker stop flask-container || exit 0'
                    bat 'docker rm flask-container || exit 0'
                    
                    // Run the new container
                    bat 'docker run -d -p 5000:5000 --name flask-container flask-app-image'
                }
            }
        }
    }
}
