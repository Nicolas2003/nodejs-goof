pipeline {
    agent any
    tools {
        nodejs 'NodeJS_22-23-2'
    }
    triggers {
        pollSCM('H/1 * * * *')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Nicolas2003/nodejs-goof.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarcloud') {
                    sh "${tool 'sonar-scanner'}/bin/sonar-scanner -Dsonar.projectVersion=${BUILD_NUMBER}"
                }
            }
        }
        stage('Build'){
            steps{
                sh 'npm run build'
            }
        }
    }
}