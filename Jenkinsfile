pipeline {
    agent any
  
    stages {
        stage('Build') { 
            steps {
                 echo 'Building'
		  sh 'git pull origin master'
		  sh 'npm install'
		  sh 'npm --version'
		  sh 'npm run build'	
                }
	    }
	    post {
		failure {
		    script {
			buildstatus = "failed"
		    }
		    echo 'Failure build'
		    emailext attachLog: false,
		    body: "Project ${env.JOB_NAME} build failed",
		    recipientProviders: [developers(), requestor()],
		    to: 'wanatwiktor08@gmail.com',
		    subject: 'Build failed'
		}
		succcess {
                    script {
                        buildstatus = "success"
                    }
		    echo 'succes build'
		    emailext attachLog: false,
                    body: "Project ${env.JOB_NAME} build success",
                    recipientProviders: [developers(), requestor()],
                    to: 'wanatwiktor08@gmail.com',
                    subject: 'Build success'
		}
            } 
        }
        stage('Test') { 
	    when {
		expression { 
		    buildstatus == 'success'
 		}
	    }
            steps {
                echo 'Testing'
                nodejs('npm') {
                    sh 'npm run test'
                }
            }
        }
    }
    post {
        success {
            echo 'Success'
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'wanatwiktor08@gmail.com',
                subject: "Succesful build in Jenkins CI"
        }
        failure {
            echo 'Fail'
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'wanatwiktor08@gmail.com',
                subject: "Failed build in Jenkins CI"
        }
    }
}
