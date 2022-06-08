pipeline {
  agent { label 'linux123' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('darinpope-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        bat 'docker build -t darinpope/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        bat 'docker push darinpope/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      bat 'docker logout'
    }
  }
}
