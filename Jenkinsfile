pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
          
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'npm test > log.txt'
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
    		attachmentsPattern: 'log.txt',
                body: "test successful",
                subject: "test successful",
                to: 'marcin.kapusta2986@gmail.com'
    	}
    	unstable{
    		echo 'Unstable....'
    		emailext attachLog: true,
    		attachmentsPattern: 'log.txt',
                body: "tests failed",
                subject: "tests failed",
                to: 'marcin.kapusta2986@gmail.com'
    	}
    }
}
