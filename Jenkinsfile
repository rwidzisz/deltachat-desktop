pipeline{
	agent any
  stages {
	  stage('Build'){
		  steps{
			  echo 'Building'
			  sh 'git pull origin master'
			  sh 'npm install'
			  sh 'npm --version'
			  sh 'npm run build'			  
		  }
	  
	  
	  post {
		failure {
		    script {
			buildstatus = 'failed'
		    }
		    echo 'Build Failed'
		    emailext attachLog: false,
		    body: "Project ${env.JOB_NAME} build failed",
		    recipientProviders: [developers(), requestor()],
		    to: 'rafal.widziszewski@gmail.com',
		    subject: 'Build failed'
		}
		succcess {
                    script {
                        buildstatus = 'success'
                    }
		    echo 'Build Successful'
		    emailext attachLog: false,
                    body: "Project ${env.JOB_NAME} build success",
                    recipientProviders: [developers(), requestor()],
                    to: 'rafal.widziszewski@gmail.com',
                    subject: 'Build success'
		}
            } 
        }
     
      stage('Test') {
      	when{
      		expression{
      			buildstatus =='success'
      		}
      	}
        steps {
              echo 'Testing'
              sh 'npm run test'
          }
      
  }
	post{
		failure{
			echo 'Test Failed'
			emailext attachLog: true,
          		body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
			to: 'rafal.widziszewski@gmail.com',
			subject: "Test failed"
		}
		success{
      			echo 'Test Successful'
      			emailext attachLog: true,
        		body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
        		to: 'rafal.widziszewski@gmail.com',
        		subject: "Test success"
		}
	}
  }
}









