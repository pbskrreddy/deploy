node {
    environment {
    
    
  }
    def mvn = tool (name: 'maven 3', type: 'maven') + '/bin/mvn'
    stage('SCM Checkout'){
   
	git 'https://github.com/krisdvs/deploy.git'
   
   }
   
   stage('Mvn Package'){
	  
	   sh "${mvn} clean package"
	   
	   
	stage('deploy_to_ans'){
	   sshagent(['ansadmin']) {
    sh "scp -r webapp/target/webapp.war ec2-user@172.31.93.153:/home/ec2-user"
  }
	}
    
   }
   stage('Build Docker Image'){
  	   sshagent(['ansadmin']) {
   
       
    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.93.153 ansible-playbook /home/ec2-user/updt_proje.yml"
 }
   }
   
   
       
    
}
