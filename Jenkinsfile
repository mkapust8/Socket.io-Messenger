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
                sh 'npm test > logs.txt'
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
    		attachmentsPattern: 'logs.txt',
                body: "test",
                subject: "test",
                to: 'marcin.kapusta2986@gmailcom'
    	}
    	unstable{
    		echo 'Sucess....'
    	}
    }
}
