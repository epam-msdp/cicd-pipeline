pipeline {
  agent {
    dockerfile {
      filename 'Dockerfile'
    }

  }
  stages {
    stage('Build Script') {
      steps {
        sh 'scripts/build.sh'
      }
    }

    stage('Test') {
      steps {
        sh 'scripts/test.sh'
      }
    }

  }
}