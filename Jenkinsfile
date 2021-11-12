pipeline {
  agent any
  stages {
    stage('Build') {
      when {
        tag 'stg-*'
      }
      steps {
        sh 'docker build -t nasrul21/devops-landing-page:$TAG_NAME .'
      }
    }

    stage('Login') {
      when {
        tag 'stg-*'
      }
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {
      when {
        tag 'stg-*'
      }
      steps {
        sh 'docker push nasrul21/devops-landing-page:latest'
      }
    }

  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred')
  }
  post {
    always {
      sh 'docker logout'
    }

  }
}