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
        
            stage( ' Build ' ){
                agent any
                     steps {
                       script {dockerImage = docker.build registryName}
                       sh 'docker tag dockerpetclinic myarureregistry.azurecr.io/ dockerpetclinic:v1 ' 
                          
             }  
                
             stage( '  Tag ' ){
                agent any
                     steps {
                      
                         echo 'bonjour'
                       //sh 'docker tag dockerpetclinic myarureregistry.azurecr.io/ dockerpetclinic:v1 ' 
                          
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
}
