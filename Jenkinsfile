pipeline {

  agent any

  environment {
          DOCKER_CREDENTIALS_ID = 'dockerhub-credentials'
          DOCKER_IMAGE = 'lashtaj/jenkins'
          KUBE_CREDENTIALS_ID = 'kubeconfig-credentials'
      }

  stages {
    stage('Build') {
          steps {
            script {
                checkout scm

                def dockerImage = docker.build('${DOCKER_IMAGE}:${env.BUILD_ID}')

                dockerImage.tag('latest')
            }
          }
        }
    stage('Push') {
          steps {
             script {
                docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                    docker.image('${DOCKER_IMAGE}:${env.BUILD_ID}').push()
                    docker.image('${DOCKER_IMAGE}:latest').push()
                }
             }
          }
    }
    stage('Publish') {
          steps {
            script {
                withCredentials([file(credentialsId: 'kubeconfig-credentials', variable: 'KUBECONFIG')]) {
                    sh 'kubectl --kubeconfig $KUBECONFIG apply -f petclinic.yml'
                }
            }
          }
    }

  }

}
