// Powered by Infostretch 


pipeline   {
        agent none
        stages {
	  stage (' Checkout') {
             agent {
               docker { 
                 image 'maven' 
                 args '-v /opt/java1:/root/.jenkins/workspace'
                 }
             }
             steps {
               echo "Checking out"
               echo " JUG checking Out"
               checkout scm
	       }
           }
	  stage ('maven - Build') {
             agent {
               docker { 
                  image 'maven'
                  args '-v /opt/java1:/root/.jenkins/workspace'   
                }
             }
             steps {
                sh '''
                  pwd && hostname	
                  cd src 
                  echo "starting the build message"> /status
	          mvn package
                '''
             } 
           }
           stage ('maven - create image') {
             agent any
             steps {
               sh '''
                 pwd && ls && hostname && cd src
                 docker build -t frontend .
               ''' 
             }
           }
           stage ('maven - deploy to docker') {
             agent any
             steps {
               sh  ''' 
                 docker rm -f angular || true
                 docker run -d -p 8000:80 --name angular frontend 
               '''
             } 
	    }  
       }
}
