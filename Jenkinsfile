// Powered by Infostretch 


node () {

	stage (' Checkout') {
         echo "Checking out"
         checkout scm
	}
	stage ('maven - Build') {
          sh ' pwd'	
          sh '  cd src '
          sh 'echo "starting the build message"> /status'
	  sh '	mvn package'
          sh ' pwd && ls '
	 sh '	docker build -t frontend . '
         //sh  ' 
           //     docker rm -f angular || true
             //   docker run -d -p 8000:80 --name angular frontend 
             //' 
	}
}
//pipeline {
//    agent any
 //   stages {
  //      stage('Build') {
   //         steps {
    //            sh 'echo "Hello world!"'
     //       }
      //  }
   // }
//}
