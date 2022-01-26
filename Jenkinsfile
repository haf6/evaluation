pipeline {
    agent any 
    environment {
        
        registry = "haf9/dockerpetclinic"
        registryCredential = 'fa32f95a-2d3e-4c7b-8f34-11bcc0191d70'
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
