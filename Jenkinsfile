pipeline {
    agent any

    environment {
        // This prevents Jenkins from killing your Flask app after the build completes
        JENKINS_NODE_COOKIE = 'dontKillMe'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Stop Existing App') {
            steps {
                // This stops any previous version of the app running on your machine
                // '|| exit 0' prevents the build from failing if no app is running
                bat 'taskkill /F /IM python.exe /T || exit 0'
            }
        }

        stage('Run Flask App') {
            steps {
                script {
                    // Starts the app in the background so Jenkins can finish the build
                    bat 'start /B python app.py'
                }
            }
        }
    }
}
