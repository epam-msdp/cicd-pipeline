pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        script {
          checkout scm
        }

      }
    }

    stage('build') {
      steps {
        sh 'cd scripts'
        sh '''
    chmod +x scripts/build.sh'''
        sh 'script scripts/build.sh'
      }
    }

    stage('test') {
      steps {
        sh 'scripts scripts/test.sh'
      }
    }

  }
}