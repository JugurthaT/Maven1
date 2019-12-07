// Powered by Infostretch 


pipeline   {
        agent none
        stages {
          stage ('cleanup') {
            agent any
            steps {
              cleanWs()
              }
          }
// the problem with this image is that it neds plugins for maven and downloads them each time
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
                  // we mount .m2 repo files to avoid maven downloading the plugins for each container
                  args '-v /root/.jenkins/workspace:/root/.jenkins/workspace -v /root/.m2:/root/.m2'   
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
             // we build docker image locally on jenkins/docker server
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
          stage ('cleanup after finish') {
            agent any
            steps {
              cleanWs()
              }
          }
 
       }
}
