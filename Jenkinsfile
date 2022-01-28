
pipeline {
    agent none
 
      
           stage ( 'Run JMeter Test' ){
                agent any
                
                steps { sh "home/hafidha/Téléchargements/apache-jmeter-5.3/bin/jmeter/sh -Jjmeter.save.saveservice.output_format=xml -n -t src/test/jmeter/petclinic_test_plan.jmx -l test.jtl"
                step([$class: 'ArtifactArchiver', artifacts: 'test.jtl'])
                perfReport 'test.jtl'
                }


           }





                


                
    
    
}
