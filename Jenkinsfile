pipeline {
  agent any
  environment {     
    DOCKERHUB_CREDENTIALS= credentials('dockerhub-credentials')     
  }
  stages {
    stage('checkout') {
        steps {
            git branch: 'main', url: 'https://github.com/ttkata/cicd-pipeline.git'
        }
    }
    stage('build') {
      steps {
        sh 'script scripts/build.sh'
      }
    }

    stage('test') {
      steps {
        sh 'script scripts/test.sh'
      }
    }

    stage('docker build') {
      steps {
        sh 'docker build -t KAN_T_image'
      }
    }
    stage('push to docker') {
      steps {
          def nodeAppDockerfilePath = 'Dockerfile'    
          // Build the Node.js app Docker image
          sh "docker build -t ttkata/KAN_T_image:$BUILD_NUMBER -f ${nodeAppDockerfilePath} ."
          sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin docker.io'                 
          sh 'docker push ttkata/KAN_T_image:$BUILD_NUMBER'                 
          sh 'docker logout'
          //docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_creds_id') { 
            //app.push("${env.BUILD_NUMBER}") 
            //app.push("latest") 
            //sh 'docker push ttkata/KAN_T_image'
          //}
      }
    }

  }
}
