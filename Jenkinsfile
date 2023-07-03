pipeline {
    agent any
    tools {nodejs "node"}
    environment { 
        switch(env.BRANCH_NAME) { 
            case "main": PORT = '3000'; break
            case "dev": PORT = '3001'; break
        }            
    }
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
                sh "docker build -t node${env.BRANCH_NAME}:v1.0 ."
            }
        }
        stage('Deploy') {
            steps {
                sh "docker run -d --expose ${PORT} -p ${PORT}:3000 node${env.BRANCH_NAME}:v1.0"
            }
        }
    }
}
