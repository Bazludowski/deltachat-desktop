pipeline {
    agent any
    
    tools { nodejs "node"}
    
    stages {
        stage('Build') { 
            steps {
                echo 'Building'
                sh 'npm install'
                sh 'npm run start'
		sh 'npm audit fix'
		sh 'npm run build'
            }
         	post {
		    failure {
		        emailext attachLog: true,
		            body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
		            recipientProviders: [developers(), requestor()],
		            to: 'zabludowskifilip@gmail.com',
		            subject: "Build failed in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
		    }
		    success {
		        emailext attachLog: true,
		            body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
		            recipientProviders: [developers(), requestor()],
		            to: 'zabludowskifilip@gmail.com',
		            subject: "Successful build in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
		    }
    		}
        }
        stage('Test') { 
            steps {
                echo 'Testing'
                sh 'npm run test'
            }
		 	post {
				failure {
				    emailext attachLog: true,
				        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
				        recipientProviders: [developers(), requestor()],
				        to: 'zabludowskifilip@gmail.com',
				        subject: "Tests failed in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
				}
				success {
				    emailext attachLog: true,
				        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
				        recipientProviders: [developers(), requestor()],
				        to: 'zabludowskifilip@gmail.com',
				        subject: "Successful testing in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
				}
    		}
        }
    }

   
}
