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
   sh 'docker build -t itsmekarthik/myweb:0.0.5'
   }
   stage('Docker Image Push'){
   withCredentials([string(credentialsId: 'dockerPass', variable: 'dockerPassword')]) {
   sh "docker login -u itsmekarthik -p ${dockerPassword}"
    }
   sh 'docker push itsmekarthik/myweb:0.0.5'
   }
