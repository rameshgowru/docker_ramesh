pipeline {
  agent {
    docker {
      image 'maven:latest'
    }

  }
  stages {
    stage('Intialization') {
      steps {
        echo 'this is testing'
      }
    }

    stage('build using maven') {
      steps {
        sh '''maven install
'''
      }
    }

  }
}