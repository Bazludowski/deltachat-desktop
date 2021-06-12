pipeline {
	agent any

	tools {nodejs "node"}

	stages {
		stage('Build') { 
		    	steps {
				checkout scm				
				echo 'Build'
				sh 'npm install'
				sh 'npm run build'
			}
		}
		stage('Test') { 
		    	steps {
		        	echo 'Test'
		            	sh 'npm run test'
		    	}
		}
		stage('Deploy'){
			steps { 
				echo 'Deploy'
				sh 'docker build -t deltachat-deploy -f Dockerfile-deploy .'
				}
			post {
				success {
					echo 'Success'
					emailext attachlog: true,
						body: "Successful Deploy"
						to: 'zabludowskifilip@gmail.com'	
						subject: "Successful deploy"		
				}
				failure {
					echo 'Failure'
					emailext attachlog: true,
						body: "Failed Deploy"
						to: 'zabludowskifilip@gmail.com'	
						subject: "Failed deploy"		
				}
}
    	}
	post {
		always {
	    		echo 'Finished'
		}
		success {
	    		echo 'Success'
			emailext attachLog: true, 
		    		body: "Success",
		    		subject: "Test Pass",
		    		to: 'zabludowskifilip@gmail.com'
		}
		failure {
			echo 'Failure'
		        emailext attachLog: true, 
		    		body: "Error:  ${env.BUILD_URL}",
		    		subject: "Test Fail",
		    		to: 'zabludowskifilip@gmail.com'
		}
	}
}
}
