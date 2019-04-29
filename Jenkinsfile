pipeline {
  agent {
    docker {
      image 'cschockaert/docker-npm-maven:1.3.0'
      args '--rm -it /bin/bash'
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
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue'
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
}