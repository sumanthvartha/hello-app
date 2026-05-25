pipeline {
    agent { label 'linux' }

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building with Maven...'
                sh 'mvn clean package'
            }
        }
        stage('Slow Stage') {
	    steps {
		echo 'Simulating a long-running build...'
		sh 'sleep 120'
		echo 'Long stage complete'
	    }
	}		
    }   

    post {
        success {
            echo 'BUILD SUCCESSFUL'
        }
        failure {
            echo 'BUILD FAILED'
        }
    }
}
