// Powered by Infostretch 

timestamps {

node () {

	stage ('npm - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '65a48dee-ef3a-462f-a0f8-eec34c6b7b1c', url: 'https://github.com/JugurthaT/frontend']]]) 
	}
	stage ('npm - Build') {
 	
// Unable to convert a build step referring to "hudson.plugins.ws__cleanup.PreBuildCleanup". Please verify and convert manually if required.		// Shell build step
sh "
		cd src
		echo "starting the build message"> /status
		mvn package
		docker build -t frontend . 
   "		
 // Shell build step
sh """ 
docker rm -f angular || true
docker run -d -p 8000:80 --name angular frontend 
 """ 
	}
}
}
