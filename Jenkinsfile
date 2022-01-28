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
           stage ( 'Run JMeter Test' ){
                agent any
                
                steps { sh "home/hafidha/Téléchargements/apache-jmeter-5.3/bin/jmeter/sh -Jjmeter.save.saveservice.output_format=xml -n -t src/test/jmeter/petclinic_test_plan.jmx -l test.jtl"
                step([$class: 'ArtifactArchiver', artifacts: 'test.jtl'])
                perfReport 'test.jtl'
                }


           }





                


                
    }
    
}
