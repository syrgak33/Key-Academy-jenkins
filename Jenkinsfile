pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {

		stage('Build') {

			steps {
				sh 'sudo docker build -t syrgak/project:latest .'
			}
		}

				
                stage('Login') {

                        steps {
                            sh 'sudo docker login -p $DOCKERHUB_CREDENTIALS_PSW -u $DOCKERHUB_CREDENTIALS_USR'
                        }
                }

		stage('Push') {

			steps {
				sh 'sudo docker push syrgak/project:latest'
			}
		}
	}
        
        post {
            always {
                sh 'sudo docker logout'
            }
        }

}
