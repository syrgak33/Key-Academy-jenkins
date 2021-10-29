pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t tynchtyk/project:latest .'
			}
		}

				
                stage('Login') {

                        steps {
                            sh 'docker login -p $DOCKERHUB_CREDENTIALS_PSW -u $DOCKERHUB_CREDENTIALS_USR'
                        }
                }

		stage('Push') {

			steps {
				sh 'docker push tynchtyk/project:latest'
			}
		}
	}
        
        post {
            always {
                sh 'docker logout'
            }
        }

}
