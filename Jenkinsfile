pipeline {
    agent {label 'On-demand-agents'}  
    
     tools {
        maven "MAVEN3"
     }
    
    stages {
    
        stage('Maven build') { 
            
            environment {
            #JAVA_OPTS="-Xms256MB -Xmx1024MB"
            MAVEN_OPTS="-Xmx1024m -XX:MaxPermSize=128m"
            }
            
            steps {
               
                  sh """
                       java -version
                       mvn install 
                     """
                
                }    

        }        
        
        stage('Docker build') {
            steps {
                    
                 sh "docker build -t petclinic:v$BUILD_NUMBER ."

            }
        }
        
        stage('Docker deploy')  {
             steps {
                    
                 sh "docker run -d -p 8000:8080 -e JAVA_OPTS='-Xms256MB -Xmx512MB' --name java-app petclinic:v$BUILD_NUMBER"

            }
        }
       
    }
}
