

pipeline {
    agent none
     
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
                    echo 'bonjour'
                   
                }
                
                         
            }
                
    }
    
}
