pipeline {
    agent any
    environment{
    	build_success = true
    	test_success = true
    }	
    stages {
    	
        stage('Build') {
            steps {
            	script{
                	try{
                		sh 'git checkout master'
                		sh 'git pull'
                		sh 'npm install'
                	}catch (Exception e){
                		build_success=false
                	}
		}
            }
        }
        stage('Test') {
            steps {
                script{
                	if(build_success)
                	{
                		try{
                			echo 'Testing..'
                			sh 'npm test > tests_log.txt'	
                		}catch (Exception e){
                			test_success=false
                		}
                	}
            	}
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post{
    	script{
	    	if(build_success){
	    		if(build_success){	
		    		echo 'Sucess....'
		    		emailext attachLog: true,
		    		attachmentsPattern: 'tests_log.txt',
				body: "Tests successful for job ${env.JOB_NAME}",
				subject: "Tests successful.",
				to: 'marcin.kapusta2986@gmail.com'
			}
			else{
		    		echo 'Unstable....'
		    		emailext attachLog: true,
		    		attachmentsPattern: 'tests_log.txt',
				body: "Tests failed for job ${env.JOB_NAME}",
				subject: "Tests failed.",
				to: 'marcin.kapusta2986@gmail.com'
		        }
	    	}
    	
    	}	
    }
}
