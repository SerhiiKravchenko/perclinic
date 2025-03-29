pipeline {

  agent any

  environment {
          DOCKER_CREDENTIALS_ID = 'dockerhub-credentials'
          DOCKER_IMAGE = "lashtaj/jenkins:${env.BUILD_ID}"
      }

  stages {
    stage('Checkout') {
          steps {
            git url:'https://github.com/SerhiiKravchenko/kube-deploy-app.git', branch:'main'
          }
    }
    stage('Build') {
          steps {
            script {
                checkout scm
                docker.build(DOCKER_IMAGE)
            }
          }
        }
    }

}
