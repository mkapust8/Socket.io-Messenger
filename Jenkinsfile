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
    		emailext body: 'Test Message',
    			subject: 'Test Subject',
    			to: 'marcin.kapusta2986@gmail.com'
    	}
    	unstable{
    		echo 'Sucess....'
    	}
    }
}
