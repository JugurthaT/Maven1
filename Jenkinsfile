// Powered by Infostretch 


pipeline   {
        agent none
	stage (' Checkout') {
           echo "Checking out"
           checkout scm
	   }
	stage ('maven - Build') {
          sh '''
               pwd	
               cd src 
               echo "starting the build message"> /status
	       mvn package
               cd src && pwd && ls
	       docker build -t frontend .
             ''' 
        }
        stage ('maven - deploy to docker') {
         sh  ''' 
                docker rm -f angular || true
                docker run -d -p 8000:80 --name angular frontend 
             ''' 
	}
}
