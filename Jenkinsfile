pipeline {
    agent { label 'linux' }

    tools {
        maven 'Maven'
    }

    environment {
        APP_NAME = 'hello-app'
        BUILD_VERSION = "1.0.${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Build: ${env.BUILD_VERSION}"
                echo "Running on: ${env.NODE_NAME}"
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Quality Gate') {
            steps {
                echo 'Quality gate check here...'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying ${APP_NAME} version ${BUILD_VERSION}"
            }
        }
    }

    post {
        success { echo "SUCCESS: ${APP_NAME} ${BUILD_VERSION}" }
        failure { echo "FAILED: Check console output" }
    }
}
