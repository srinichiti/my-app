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
stage('Docker Build and Image') {
           steps {              
	 sh "docker build -t itsmekarthik/testing:${BUILD_NUMBER} ."                            
          }
        }
stage('Docker Login') {
           steps { 
		   withCredentials([string(credentialsId: 'Dockerid', variable: 'Dockerpwd')]) {
	sh "docker login -u itsmekarthik -p ${Dockerpwd}" 
}
		                             
          }
        }
stage('Push to Repository') {
           steps {              
	 sh "docker push -t itsmekarthik/testing:${BUILD_NUMBER}"                            
          }
        }
