pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'NodeJS 14', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/abdullahzahid39/Basic-calculator.git'
            }
        }

    
        stage('Build and Start Application with Docker Compose') {
            steps {
                script {
                    sh 'docker-compose build'
                    sh 'docker-compose up'
                }
            }

            post {
                success {
                    echo 'Application is up and running in the background'
                }
                failure {
                    error('Failed to start application')
                }
            }
        }
    }
}
