pipeline {
  agent any
  stages {
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
        script {
          def nodeAppDockerfilePath = 'src/Dockerfile'
          // Build the Node.js app Docker image
          sh "docker build -t ttkata/KAN_T_image:$BUILD_NUMBER -f ${nodeAppDockerfilePath} ."
          sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin docker.io'
          sh 'docker push ttkata/KAN_T_image:$BUILD_NUMBER'
          sh 'docker logout'
        }

      }
    }

  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dhub')
  }
}
