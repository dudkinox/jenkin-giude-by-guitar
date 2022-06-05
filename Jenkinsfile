pipeline {
    agent any

    stages {
        stage('confirm version') {
            steps {
                nodejs('Node17.9') {
                    sh 'node -v'
                    sh 'npm -v'
                }
            }
        }
        stage('install node packages') {
            steps {
                nodejs('Node17.9') {
                    sh 'npm install'
                }
            }
        }
    }
}
