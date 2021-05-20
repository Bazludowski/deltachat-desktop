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
