pipeline {
    agent any
    tools {nodejs "node"}
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'CI=true npm test'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "docker build -t node${env.BRANCH_NAME}:v1.0"
            }
        }
        stage('Deploy') {
            steps {
                sh "docker run -d --expose 3000 -p 3000:3000 node${env.BRANCH_NAME}:v1.0"
            }
        }
    }
}
