pipeline {
    agent none
    
    
    
    
     
    stages {    
            
        stage('Hello') 
        {   agent any 
            steps {
                echo 'Hello World'
                sh 'docker ps -aq | xargs --no-run-if-empty docker stop' 
                echo ' remove all docker containers' 
                sh 'docker ps -aq | xargs --no-run-if-empty docker rm'
               
                  }
            
        }
        
        
        
        
            stage( ' Build - Maven package ' ){
                agent any
                     steps {
                       echo 'bonjour'
                       sh ' mvn -version '
                        sh 'mvn clean package -P MySQL '  
                }
                     
                       
            }
        
            stage( ' Generate docker application image ' ){
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
