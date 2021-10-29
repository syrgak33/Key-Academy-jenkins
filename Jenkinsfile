pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred-menin')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t tynchtyk/project:latest .'
			}
		}

				}

		stage('Push') {

			steps {
				sh 'docker push tynchtyk/project:latest'
			}
		}
	}

	

}
