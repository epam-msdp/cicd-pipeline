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
                sh "docker build -t node${env.BRANCH_NAME}:v1.0 ."
            }
        }
        stage('Deploy') {
            steps {
                script {
                    def PORT
                    switch(env.BRANCH_NAME) { 
                        case "main": PORT = '3000'; break
                        case "dev": PORT = '3001'; break
                    }            
                    sh "docker rm -f node${env.BRANCH_NAME} || echo 'No container found'"
                    sh "docker run -d --name node${env.BRANCH_NAME} --expose ${PORT} -p ${PORT}:3000 node${env.BRANCH_NAME}:v1.0"
                }
            }
        }
    }
}
