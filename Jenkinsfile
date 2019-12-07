// Powered by Infostretch 


pipeline   {
        agent none
        stages {
          stage ('cleanup') {
            agent any
            steps {
              cleanws()
              }
          }
	  stage (' Checkout') {
             agent {
               docker { 
                 image 'maven' 
                 args '-v /root/.jenkins/workspace:/root/.jenkins/workspace'
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
                  args '-v /root/.jenkins/workspace:/root/.jenkins/workspace'   
                }
             }
             steps {
                sh '''
                  pwd && hostname && df -h	
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
