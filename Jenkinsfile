node{
   stage('SCM Checkout'){
     git 'https://github.com/kkarthikrj/my-app.git'
      }
   stage('maven-buildstage'){
      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
        }
   stage('Build Docker Image'){           
	 sh 'docker build -t itsmekarthik/my-app:0.0.2 .' 
	   }
	stage('Push Docker Image'){   
	withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhubpwd')]) {
	sh "docker login -u itsmekarthik -p ${dockerhubpwd}"	
           }
	sh 'docker push -t itsmekarthik/my-app:0.0.2'	
           }
          }
           
