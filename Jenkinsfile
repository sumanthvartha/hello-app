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
                echo "Starting optimized build - Optimization 2: Maven flags"
            }
        }

        stage('Build') {
            steps {
                // Optimization: skip tests here (separate stage)
                // skip javadoc, skip source jar, use 2 threads
                sh '''
                    mvn clean package \
                    -DskipTests \
                    -Dmaven.javadoc.skip=true \
                    -Dmaven.source.skip=true \
                    -T 2
                '''
            }
        }

        stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Quality Checks') {
            parallel {
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
            }
        }

        stage('Package Final') {
            steps {
                // Also optimized: no docs, no source jar
                sh 'mvn package -DskipTests -Dmaven.javadoc.skip=true -T 2'
            }
        }
    }

    post {
        always {
            echo "BUILD COMPLETE"
        }
    }
}
