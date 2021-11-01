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

}
