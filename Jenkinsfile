// Powered by Infostretch 


//node () {
//
//	stage ('npm - Checkout') {
//         echo "Checking out"
//	}
//	stage ('npm - Build') {
// 	
//sh "
//		cd src
//		echo "starting the build message"> /status
//		mvn package
//		docker build -t frontend . 
 //  "		
 // Shell build step
//sh """ 
//docker rm -f angular || true
//docker run -d -p 8000:80 --name angular frontend 
// """ 
//	}
//}
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello world!"'
            }
        }
    }
}
