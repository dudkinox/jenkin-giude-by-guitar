# jenkin-101
```
pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                git branch: 'main', url: 'https://github.com/dudkinox/jenkin-101'
            }
        }
        stage('Docker image') { 
            steps {
                sh "echo Docker image"
            }
        }
        stage('Deploy') { 
            steps {
                sh "echo Deploy"
            }
        }
        stage('Discord noti') { 
            steps {
                sh "echo Discord noti"
            }
        }
    }
}
```
