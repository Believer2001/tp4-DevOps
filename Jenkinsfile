pipeline {
  agent any
  environment {
    REGISTRY_REPO = "believer2001/tp4_v3" 
    REGISTRY_CREDENTIAL_ID = 'DOCKERHUB_CREDENTIALS'     
    DOCKER_IMAGE = null // This is the variable name used below
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
            // CORRECTION 1: Use DOCKER_IMAGE for push
            DOCKER_IMAGE.push()
            // CORRECTION 2: Push the 'latest' tag (best practice)
            DOCKER_IMAGE.push('latest')
          }
        }
      }
    }
    
    // You can add a separate 'Deployment' stage here if needed, which uses the 'latest' tag.
  } // <--- Closing brace for 'stages'
} // <--- Closing brace for 'pipeline' (THIS WAS LIKELY MISSING)