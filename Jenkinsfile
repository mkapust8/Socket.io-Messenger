pipeline {
    agent any
    environment{
    	build_success = true
    	test_success = true
    }
    stages {
        stage('Build') {
            steps {
                sh 'git checkout master'
                sh 'git pull'
                sh 'npm install'
            }
            post {
            	
            	failure{
            		script{
            			build_success = false
            			echo 'Build failed....'
			    	emailext attachLog: true,
				body: "Build failed for job ${env.JOB_NAME}",
				subject: "Build failed.",
				to: 'marcin.kapusta2986@gmail.com'
            		}
            	}
            	success{
            		echo 'Build success....'
			emailext attachLog: true,
			body: "Builds succeeded for job ${env.JOB_NAME}",
			subject: "Build sucess.",
			to: 'marcin.kapusta2986@gmail.com'
            	}
            
            }
        }
        stage('Test') {
            steps {
            	script{
            		if(build_success)
            		{
				echo 'Testing..'
				sh 'npm test > tests_log.txt'
			}
                }
            }
            post {
            	
            	failure{
            		script{
            			test_success = false
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
    	always{
	    	script{
	    		if(build_success){
	    			if(test_success){
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
}
