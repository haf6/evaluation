
pipeline {
    agent none
 
        environment {
        registryName = 'myarureregistry'
        registryUrl = 'myarureregistry.azurecr.io'
        registryCredential = 'ACR'
        dockerImage = ' '
        }
    
    stages {    
            
            stage( ' Build - Maven package ' ){
                agent any
                     steps {
                       echo 'bonjour'
                       sh ' mvn -version '
                        sh 'mvn clean package -P MySQL '  
                }
                     
                       
            }
        
            stage( 'Build Docker Image  ' ){
                agent any
                     steps {
                       script {dockerImage = docker.build registryName}
                       
                          
                }    
                         
            }

            stage( ' tag image ' ){
                 agent any
                     steps {
                    sh 'docker tag myarureregistry   myarureregistry.azurecr.io/petclinic:v1 ' 
                                
                                    
                            }    
                                    
            }





            stage( 'Upload Image to ACR ' ){
              
                steps{ 

                     script {
                         docker.withRegistry( "http://${registryUrl}", registryCredential ) {

                        dockerImage.push()} 
                   
                }
                         
            }
            
                
    }
    
}

