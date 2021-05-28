pipeline{
	agent any
  stages {
	  stage('Build'){
		  steps{
			  echo 'Building'
			  sh 'git pull origin master'
			  //sh 'npm install'
			  //sh 'npm --version'
			  //sh 'npm run build'
			  script {
			  	last_stage = env.STAGE_NAME
			  }			  
		  }
	}
   
      stage('Test') {
        steps {
        
        	script{
        		last_stage=env.STAGE_NAME
        		if("${currentBuild.currentResult}"=='SUCCESS')
        		{
        			echo 'Testing'
              			//sh 'npm run test'
              		}
              		else
              		{
              		echo "Build:${currentBuild.currentResult}"
              		}
          	}
      
  	}
  }
stage('Deploy'){
  	steps{
  		echo 'Deploying..'
  		//sh 'docker build -t deploy -f kouminkator-deploy .'
  }
  
  
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

