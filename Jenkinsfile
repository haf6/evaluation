




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
                       script {dockerImage = docker.build registryName}
                       
                          
                }    
                         
            }
            stage( 'Upload Image to ACR ' ){
              
                steps{ 

                     script {
                         docker.withRegistry( "http://${registryUrl}", registryCredential ) {

                        dockerImage.push()} 
                   
                }
                          
            }

            stage('stop previous containers') {
                steps {
                    sh 'docker ps -f name=mypythonContainer -q | xargs --no-run-if-empty docker container stop'
                    sh 'docker container ls -a -fname=mypythonContainer -q | xargs -r docker container rm'
                }
            }
            
            stage('Docker Run') {
            steps{
                script {
                        sh 'docker run -d -p 8096:5000 --rm --name mypythonContainer ${registryUrl}/${registryName}'
                    }
            }









                
    }
    
}
}









