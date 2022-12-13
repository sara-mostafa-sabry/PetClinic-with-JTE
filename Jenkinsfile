pipeline {
    agent {label 'On-demand-agents'}  
    
    stages {
    
        stage('Maven build') { 
            
            steps {
               
                  sh """
                       java -version 
                       mvn -version
                       ./mvnw package 
                     """
                
                }    

        }        
        
        stage('Docker build') {
            steps {
                    
                 sh "docker build -t petclinic:v$BUILD_NUMBER spring-petclinic-app/Dockerfile "

            }
        }
        
        stage('Docker deploy')  {
             steps {
                    
                 sh "docker run -d -p 8000:8080 -e JAVA_OPTS='-Xms256MB -Xmx512MB' -v /var/run/docker.sock:/var/run/docker.sock --name java-app petclinic:v$BUILD_NUMBER"

            }
        }
       
    }
}
