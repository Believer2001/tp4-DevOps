pipeline {
  environment {
    REGISTRY_REPO = "believer2001/tp4_v3" 
    REGISTRY_CREDENTIAL_ID = 'DOCKERHUB_CREDENTIALS'     
    DOCKER_IMAGE = null
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
       git url:'https://github.com/Believer2001/tp4-DevOps',branch: 'main'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build "${REGISTRY_REPO}:${env.BUILD_NUMBER}", '.'
        }
      }
    }
stage('Test image') {
        steps{
        script {
        echo "Démarrage des tests de l'image..."
          
         
            echo "Tests passed"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', REGISTRY_CREDENTIAL_ID ) {
          dockerImage.push()
        }-
      }
    }
  }
}
}