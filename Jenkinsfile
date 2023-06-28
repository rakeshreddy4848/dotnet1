pipeline {
  agent any
  stages {

    stage('Docker build and push') {
      steps {
		sh '''
		 whoami
		 #aws configure set aws_access_key_id $ACCESS_KEY
		 #aws configure set aws_secret_access_key $ACCESS_SECRET_KEY
		 #aws configure set default.region us-east-2
		 aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 462693274005.dkr.ecr.us-east-2.amazonaws.com
		 docker build -t docker1 .
		 docker tag docker1:latest 462693274005.dkr.ecr.us-east-2.amazonaws.com/docker1:${BUILD_NUMBER}
		 docker push 462693274005.dkr.ecr.us-east-2.amazonaws.com/docker1:${BUILD_NUMBER}
		  '''
	     }	         
	   }

    stage('Deploy docker'){
      steps {
		sh '''
			  ssh -i /var/lib/jenkins/.ssh/jenkins-practice.pem -o StrictHostKeyChecking=no ubuntu@ec2-18-117-146-110.us-east-2.compute.amazonaws.com 'bash -s' < ./deploy.sh \${BUILD_NUMBER}
			  '''	 
		    
      		}
		}		    

}

 }
