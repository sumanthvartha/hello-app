pipeline {
    agent { label 'linux' }

    tools {
        maven 'Maven'
    }

    options {
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "Starting baseline build"
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Simulating SonarQube scan...'
                sh 'sleep 10'
                echo 'Code Analysis complete'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Simulating OWASP scan...'
                sh 'sleep 12'
                echo 'Security Scan complete'
            }
        }

        stage('Generate Docs') {
            steps {
                sh 'mvn javadoc:javadoc'
            }
        }

        stage('Package Final') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
    }

    post {
        always {
            echo "BUILD COMPLETE"
        }
    }
}
