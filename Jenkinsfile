node{
   stage('SCM Checkout'){
     git 'https://github.com/srinichiti/my-app.git'
      }
   stage('maven-buildstage'){
      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
   }
}
