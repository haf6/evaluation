
 

pipeline {
    agent none
 
    environment {
       registryName = " myContainerAzureRegistry"
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
            stage( 'deployment vers azure registry  ' ){
                 agent any
                     steps {
                       echo 'bonjour'
                         #sh ' az login '

                         #sh ' az acr login --name myContainerAzureRegistry '
                        # sh ' docker tag dockerpetclinic mycontainerazureregistry.azurecr.io/dockerpetclinic:v01'

                     
                         
                    }    
                         
            }
                
   }
    
}




























