pipeline {
    agent any
    tools{
    	nodejs "NodeJS"
    }
    stages{
   
        stage('Test') {
            steps {		
            	echo ‘Test start’
		sh 'npm install'
		sh 'npm --version'
		sh 'npm run test'
                 
            }
        }
        
    }
    post{
        failure{
        	echo 'Failed Test'
        	emailtext attachLog: true,
        		body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
					to: 'rafal.widziszewski@gmail.com',
        				subject: 'Jenkins Test Failure'
        } 	
        success{
        	echo 'Sucessful Test'
        	emailtext attachLog: true,
       	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
					to: 'rafal.widziszewski@gmail.com',
        				subject: 'Jenkins Test Sucess'	
		}		
	}
}
