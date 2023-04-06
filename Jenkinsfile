node{
   stage('SCM Checkout'){
     git 'https://github.com/kkarthikrj/my-app.git'
   }
   stage('maven-buildstage'){
      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
}
stage('Build Docker Image'){
   sh 'docker build -t itsmekarthik/testing'
   }
   stage('Docker Image Push'){
   withCredentials([string(credentialsId: 'dockerPass', variable: 'docker-hub-karthik')]) {
   sh "docker login -u itsmekarthik -p ${dockerPassword}"
    }
   sh 'docker push itsmekarthik/testing'
   }
stage('Nexus Image Push'){
   sh "docker login -u admin -p admin123 13.126.139.197:8083"
   sh "docker tag itsmekarthik/testing 13.126.139.197:8083/karthik:1.0.0"
   sh 'docker push 13.126.139.197:8083/karthik:1.0.0'
   }

   stage('Remove Previous Container'){
	try{
		sh 'docker rm -f tomcattest'
	}catch(error){
		//  do nothing if there is an exception
	}
   stage('Docker deployment'){
   sh 'docker run -d -p 8090:8080 --name tomcattest itsmekarthik/testing' 
   }
}
