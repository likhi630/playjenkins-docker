pipeline {

  environment {
    registry = "likhi63/bootcamp"
    registryCredential = 'dockerhub1'
    dockerImage = ""
  }

  agent any

  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/likhi630/playjenkins-docker.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":latest"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "", registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:latest"
      }
    }

    stage('Deploy App') {      
        steps{
        sh "docker run -d -it -p 80:80 $registry:latest"
      }      
    }
  }
}
