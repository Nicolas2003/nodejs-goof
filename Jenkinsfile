pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Verify') {
            steps {
                sh 'git log -1 --oneline'
                sh 'ls -la'
                sh 'cat package.json'
            }
        }
    }
}