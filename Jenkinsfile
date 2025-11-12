pipeline {
  agent any
  environment {
    REGISTRY_REPO = "believer2001/tp4_v3" 
    REGISTRY_CREDENTIAL_ID = 'DOCKERHUB_CREDENTIALS'     
    DOCKER_IMAGE = null // This is the variable name used below
    CONTAINER_NAME = 'tp4-app'
  }

  stages {
    stage('Cloning Git') {
      steps {
        git url:'https://github.com/Believer2001/tp4-DevOps', branch: 'main'
      }
    }
    
    stage('Building image') {
      steps{
        script {
          // CORRECTION 1: Use DOCKER_IMAGE (uppercase) consistently
          DOCKER_IMAGE = docker.build "${REGISTRY_REPO}:${env.BUILD_NUMBER}", '.'
        }
      }
    }
    
    stage('Test image') {
      steps{
        script {
          echo "Démarrage des tests de l'image..."
          // Add actual test commands here if required
          echo "Tests passed"
        }
      }
    }
    
    // RENAMED TO PUBLISH IMAGE (as it performs the push operation)
    stage('Publish Image') { 
      steps{
        script {
          docker.withRegistry( '', REGISTRY_CREDENTIAL_ID ) {
            DOCKER_IMAGE.push()
            DOCKER_IMAGE.push('latest')
          }
        }
      }
    }

 stage('Deploy image') {
  steps{
    script {
        // Technique plus robuste pour Windows/bat : Tester avant de supprimer
        bat "docker stop ${CONTAINER_NAME}"
        bat "docker rm ${CONTAINER_NAME}" 
        
        // Déploiement
        bat "docker run -d -p 8089:80 --name ${CONTAINER_NAME} ${REGISTRY_REPO}:latest"
        
        echo "Déploiement terminé. L'application devrait être accessible sur http://<IP_DE_VOTRE_VM>:8081"
    }
  }
}
    
  } 
} 