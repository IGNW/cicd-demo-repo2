pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '''-p 3000:3000
-u 0:0'''
    }

  }
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'npm install'
          }
        }
        stage('Secrets Injection') {
          steps {
            echo 'Secrets retrieved here'
          }
        }
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          environment {
            CI = 'true'
          }
          steps {
            sh './jenkins/scripts/test.sh'
            echo 'Made it to test test test'
            echo 'Hi Noah'
          }
        }
        stage('Artifactory') {
          steps {
            echo 'I am delievering an Artifact'
          }
        }
      }
    }
    stage('Deliver') {
      parallel {
        stage('Deliver') {
          steps {
            sh './jenkins/scripts/deliver.sh'
            input 'Finished using the web site? (Click "Proceed" to continue)'
            sh './jenkins/scripts/kill.sh'
          }
        }
        stage('Carlos') {
          steps {
            echo 'Hi Carlos!'
          }
        }
      }
    }
  }
}