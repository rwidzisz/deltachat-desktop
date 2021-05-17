pipeline{
	agent any
  stages {
	  stage('Build'){
		  steps{
			  echo 'Building'
			  sh 'git pull origin master'
			  nodejs('npm')
			  {
			 	sh 'npm install'
			  }		  
			  sh 'npm --version'
			  sh 'npm run build'			  
		  }
	  }
     
      stage('Test') {
          steps {
              echo 'Testing'
              sh 'npm run test'
          }
      }
  }
	post{
		failure{
				echo 'Test failed'
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
