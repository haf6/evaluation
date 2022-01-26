pipeline {
    agent any 
    environment {
        
        registry = "haf9/dockerpetclinic"
        dockerImage = ''
    }
    
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }
