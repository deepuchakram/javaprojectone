pipeline {
  environment {
    registry = "sudeepthi/javaprojectone"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  tools { 
    nodejs "node"
  }
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/deepuchakram/javaprojectone.git'
      }
    }
    stage('Build') {
       steps {
         shell 'npm install'
         shell 'npm run bowerInstall'
       }
    }
    stage('Test') {
      steps {
        shell 'npm test'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}
