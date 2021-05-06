pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                try{
                	sh 'git checkout master'
                	sh 'git pull'
                	sh 'npm install'
                }catch (Exception e){
                	build_success=false
                }
          
            }
        }
        stage('Test') {
            steps {
                if(build_success)
                {
                	echo 'Testing..'
                	sh 'npm test > tests_log.txt'	
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
    	success {
    		echo 'Sucess....'
    		emailext attachLog: true,
    		attachmentsPattern: 'tests_log.txt',
                body: "Tests successful for job ${env.JOB_NAME}",
                subject: "Tests successful.",
                to: 'marcin.kapusta2986@gmail.com'
    	}
    	unstable{
    		echo 'Unstable....'
    		emailext attachLog: true,
    		attachmentsPattern: 'tests_log.txt',
                body: "Tests failed for job ${env.JOB_NAME}",
                subject: "Tests failed.",
                to: 'marcin.kapusta2986@gmail.com'
    	}
    }
}
