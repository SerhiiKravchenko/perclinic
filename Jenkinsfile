pipeline {

  agent any

  environment {
          DOCKER_CREDENTIALS_ID = 'dockerhub-credentials'
          DOCKER_IMAGE = "lashtaj/jenkins:${env.BUILD_ID}"
      }

  stages {
//     stage('Checkout') {
//           steps {
//             git url:'https://github.com/SerhiiKravchenko/perclinic.git', branch:'main'
//           }
//     }
//     stage('Build') {
//           steps {
//             script {
//                 checkout scm
//                 docker.build(DOCKER_IMAGE)
//             }
//           }
//         }
//     stage('Push') {
//           steps {
//              script {
//                 docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
//                     docker.image(DOCKER_IMAGE).push()
//                 }
//              }
//           }
//     }
    stage('Publish') {
//           agent {
//             label 'jenkins'
//           }
          steps {
            script {
              kubernetesDeploy(configs: 'petclinic.yml', kubeconfigId: 'k8config')
            }
          }
    }

  }

}
