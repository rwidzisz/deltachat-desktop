pipeline {
    agent any
	tools{
		nodejs "NodeJS"	
	}

    stages{
    
    	stage('Build'){
    	steps{
    		echo 'Build start'
    		sh 'npm install'
    		sh 'npm run build'
    		}
    	}	  
        stage('Test') {
            steps {		
            	echo ‘Test_start’
		sh 'npm run test'
                 
            }
        }
        
    }
    post{
        failure{
        	echo 'Failed Test'
        	emailext attachLog: true,
        		body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
					to: 'rafal.widziszewski@gmail.com',
        				subject: 'Jenkins Test Failure'
        } 	
        success{
        	echo 'Sucessful Test'
        	emailext attachLog: true,
       	body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
					to: 'rafal.widziszewski@gmail.com',
        				subject: 'Jenkins Test Sucess'	
		}		
	}
}
