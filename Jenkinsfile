
pipeline 
{
    agent none
    environment
    {
        MYSQL_SERVER_IP='sq1.mysql.database.azure.com'
        MYSQL_USERNAME='hafidha'
        MYSQL_PASSWORD='hamouda@@1981'
    }
    stages 
    {

        stage('Hello') 
        {   agent any 
            steps {
                echo 'Hello World'
                sh 'docker ps -aq | xargs --no-run-if-empty docker stop' 
                echo ' remove all docker containers' 
                sh 'docker ps -aq | xargs --no-run-if-empty docker rm'
               
                  }
            
        }
        
       
        stage('Docker Maven: tests et package ')  
        { 
            agent
            {  
                 docker { image 'maven:3.8.4-jdk-amd64' }  
            } 
            steps  
            { 
                    echo 'Building stage'
                    sh 'mvn --version'
                    sh 'mvn clean '
                    sh 'mvn -Denv.MYSQL_SERVER_IP=${MYSQL_SERVER_IP}  -Denv.MYSQL_USERNAME=${MYSQL_USERNAME} -Denv.MYSQL_PASSWORD=${MYSQL_PASSWORD} package -P MySQL '


 
            } 
        }
        stage('build imageDocker') 
        {   agent any 
            steps {
              sh 'docker build -t petclinic:v01 .'
              sh ' docker run --network="host" -d --name petclinic petclinic:v01 '

               
                  }
            
        }
    }
}

