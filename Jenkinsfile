pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        echo 'installing npm in Build stage'
      }
    }

    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
        echo 'Running test in Test stage'
      }
    }

    stage('Dliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
}