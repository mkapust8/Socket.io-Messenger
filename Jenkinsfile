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
    	}
    	failure{
    		echo 'Sucess....'
    	}
    }
}
