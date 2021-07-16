pipeline {
    agent  { label 'slave2'}
    stages {
        stage(cloneProject) {
            steps {
                sh 'cd /home/slave2/'
                sh 'git clone https://github.com/Manjunathhm/java-mvn-hello-world-web-app.git'
                sh 'pwd'
                sh 'cd /home/slave2/workspace/ProjectOne'
            }
        }
        stage(BuildProcess) {
  		steps {
                	sh 'cd /home/slave2/workspace/ProjectOne'
                  	sh 'sudo docker build -t mavenbuild /home/slave2/workspace/ProjectOne'
			sh 'sudo docker tag mavenbuild:latest 155635587501.dkr.ecr.us-east-2.amazonaws.com/private_repo1:latest'
                        sh 'sudo docker push 155635587501.dkr.ecr.us-east-2.amazonaws.com/private_repo1:latest'
            	}
	}
         stage(DeployProcess) {
           steps {
                    sh 'cd /home/slave2/workspace/ProjectOne'
                    sh 'sudo docker run -d -p 8090:8080 mavenbuild:latest'
		}
	   }
	}
}
