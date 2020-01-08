node {
    environment {
    registry = "krishna471/pipe_1"
    registryCredential = 'dockerhub'
    
  }
    def mvn = tool (name: 'maven 3', type: 'maven') + '/bin/mvn'
    stage('SCM Checkout'){
   
	git 'https://github.com/krisdvs/deploy.git'
   
   }
   
   stage('Mvn Package'){
	  
	   sh "${mvn} clean package"
	   
	   
	stage('deploy_to_ans'){
	   sshagent(['ansadmin']) {
    sh "scp -r webapp/target/webapp.war ec2-user@172.31.93.153:/home/ansadmin"
  }
	}
    
   }
   stage('Build Docker Image'){
  	   sshagent(['ansadmin']) {
   
       
    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.93.153 docker build https://github.com/krisdvs/deploy.git#Dockerfile "
 }
   }
   stage('docker container'){
      sshagent(['ansadmin']) {
   def dockerRun = 'docker run -d -p 8080:8080 --name myweb krishna-devimg '
   
    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.93.153 ${dockerRun}"
   }
   }
   
       
    
}
