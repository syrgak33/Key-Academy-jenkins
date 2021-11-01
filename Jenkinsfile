pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {

		stage('Build') {

			steps {
				sh 'sudo docker build -t foracloud/syrgak:latest .'
			}
		}

				
                stage('Login') {

                        steps {
                            sh 'sudo docker login -p $DOCKERHUB_CREDENTIALS_PSW -u $DOCKERHUB_CREDENTIALS_USR'
                        }
                }

		stage('Push') {

			steps {
				sh 'sudo docker push foracloud/syrgak:latest'
			}
		}
	}
        
        post {
            always {
                sh 'sudo docker logout'
            
	    
	    
	    }
        }
	stage ('Deploy to staging') {
  
    steps {
        withCredentials ([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
            script {
                sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@${env.stage_ip} \"docker pull foracloud/syrgak:latest\""
                try {
                   sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@${env.stage_ip} \"docker stop train-schedule\""
                   sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@${env.stage_ip} \"docker rm train-schedule\""
                } catch (err) {
                    echo: 'caught error: $err'
                }
                sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@${env.stage_ip} \"docker run --restart always --name train-schedule -p 80:8080 -d foracloud/syrgak:latest\""
            }
        }
    }
}
stage ('Deploy to production') {
  
    steps {
        input 'Deploy to Production?'
        milestone(1)
        withCredentials ([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
            script {
                sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@${env.prod_ip} \"docker pull foracloud/syrgak:latest\""
                try {
                   sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@${env.prod_ip} \"docker stop train-schedule\""
                   sh "sshpass -p '$USERPASS' -v ssh -o StrictHostKeyChecking=no $USERNAME@${env.prod_ip} \"docker rm train-schedule\""
                } catch (err) {
                    echo: 'caught error: $err'
                }
                sh "sshpass -p '$USERPASS' -v
	

}

