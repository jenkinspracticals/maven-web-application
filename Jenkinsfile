pipeline{

agent any

tools
{
  maven 'maven3.8.3'

}

triggers{
 pollSCM('* * * * *')
}

options{
    timestamps()
    buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '2', daysToKeepStr: '', numToKeepStr: '2'))
}

 stages{
   
   stage('CheckoutCode')
   {
     steps{
	git credentialsId: '790d9d01-86d2-48df-b2a9-72f18105394b', url: 'https://github.com/jenkinspracticals/maven-web-application.git'
	 }
   }
   
   stage('Build')
   {
    steps{
	  sh "mvn clean package"
	 }
   }
   
    stage('ExecuteSonarQubeReport')
   {
     steps{
	  sh "mvn sonar:sonar"
	 }
   }
   
   stage('UploadArtifactintoNexus')
   {
     steps{
	  sh "mvn deploy"
	 }
   }
   
  stage('DeployAppIntoTomcat')
 {
   steps{
  
  sshagent(['9ea72a9a-4a54-48dd-92be-163befb388b6']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.19.11:/opt/apache-tomcat-9.0.53/webapps"
}
  
 }
 }
 
  
 
 }
 /*
 post{
 
 
 success{
 mail bcc: 'devopstrainingblr@gmail.com', body: '''BuildOver!....

 Regards,
 Mithun Technologies,
 9980923226''', cc: 'devopstrainingblr@gmail.com', from: '', replyTo: '', subject: 'BuildOver!!', to: 'devopstrainingblr@gmail.com'
 }
 
 failure{
 mail bcc: 'devopstrainingblr@gmail.com', body: '''BuildOver!....

 Regards,
 Mithun Technologies,
 9980923226''', cc: 'devopstrainingblr@gmail.com', from: '', replyTo: '', subject: 'BuildOver!!', to: 'devopstrainingblr@gmail.com'
 }
 
 }
 */
}
