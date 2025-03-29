pipeline {

  agent any

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
