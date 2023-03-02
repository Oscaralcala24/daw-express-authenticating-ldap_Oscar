pipeline {
  agent {
    docker {
      args '-p 3000:3000'
      image 'node:lts-buster-slim'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      environment {
        CI = 'true'
      }
      steps {
        sh 'npm test'
      }
    }

    stage('Deliver') {
      steps {
        sh ' sudo ./jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Select "Proceed" to continue)'
        sh 'sudo ./jenkins/scripts/kill.sh'
      }
    }

  }
}