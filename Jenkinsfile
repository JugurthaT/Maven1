// Powered by Infostretch 


pipeline   {
        agent none
        stages {
	  stage (' Checkout') {
             agent node:7-alpine
             steps {
               echo "Checking out"
               checkout scm
	       }
           }
	  stage ('maven - Build') {
             agent node:7-alpine
             steps {
                sh '''
                  pwd	
                  cd src 
                  echo "starting the build message"> /status
	          mvn package
                  cd src && pwd && ls
	          docker build -t frontend .
                '''
             } 
           }
           stage ('maven - deploy to docker') {
             agent node:7-alpine
             steps {
               sh  ''' 
                 docker rm -f angular || true
                 docker run -d -p 8000:80 --name angular frontend 
               '''
             } 
	    }  
       }
}
