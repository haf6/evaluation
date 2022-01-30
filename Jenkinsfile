
pipeline{
    agent none
 
        environment {
        registryName = 'myarureregistry'
        registryUrl = 'myarureregistry.azurecr.io'
        registryCredential = 'ACR'
        dockerImage = ' '
        }
    
    stages{     
            
            stage( ' Build - Maven package ' ){
                agent any
                     steps {
                       echo 'bonjour'
                       sh ' mvn -version '
                        sh 'mvn clean package -P MySQL '  
                }
                 
            }  
            stage ( 'Run JMeter Test' ){
                agent any
                
                    steps { sh "/home/hafidha/Téléchargements/apache-jmeter-5.3/bin/jmeter  -Jjmeter.save.saveservice.output_format=xml -n -t src/test/jmeter/petclinic_test_plan.jmx -l test.jtl"
                   
                      step([$class: 'ArtifactArchiver', artifacts: 'test.jtl'])
                      perfReport 'test.jtl'

                    }

            }

                       
           
        
            stage( ' Build image ' ){
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
                         
            }
            stage('Prepare Environment') {
                
                agent any
                
                steps
                    {
                
                        sh 'az login --service-principal -u 7397d218-0fa4-40dd-948d-2b59227171ef -p peTgrh2jlvKGd_sZ76nbOb4X_XYzc1Try3 -t d1859195-72dc-49c3-a815-5d4106a85dfb'
                        
                        sh 'az aks get-credentials --resource-group mongroupeaks  --name aksclusterPC  --overwrite-existing'
                    }
            }      
                    

            stage('Deploy') {
                agent any
                
                    steps
                    {
                    sh 'kubectl apply -f fichier.yaml '
                    }
                
            }


                
    }    
    
}
       
