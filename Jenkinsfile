
pipeline{

   agent any

	//create dockerhub credential in github with TOKEN
	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
	
	stages {

		stage('gitclone') {

		      steps {
		         git https://github.com/Omegawonder/NovClass.git
		      }
		}
		
		stage('Build') {
			steps {
			
			   sh 'docker build -t omegawonder:${BUILD_NUMBER} .'
			}
		}
		
		stage('Login') {
		
			steps {
			   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username omegawonder --password-stdin'    
			}
		}

		stage('Push') {
			
			steps {
			   sh 'docker push omegawonder:${BUILD_NUMBER}'
			}
		}
		}
	
	post {
	    always {
		sh 'docker logout'
	    }
    }

}

