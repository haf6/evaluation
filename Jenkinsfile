
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
        
            stage( ' génerer image docker application ' ){
                agent any
                     steps {
                       echo 'bonjour'
                       sh ' docker build -t dockerpetclinic:v01 . '
                         
                }    
                         
            }
            stage( 'Upload Image to ACR ' ){
              
                steps{   
                    sh 'docker.withRegistry( "http://${registryUrl}", registryCredential ) {
                        dockerpetclinic:v01.push()'
                    
                }
                
                         
            }
                
    }
    
}

