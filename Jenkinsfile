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

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Start Application with PM2') {
            steps {
                sh 'npm install -g pm2' // Install PM2 globally if not already installed
                sh 'pm2 start npm -- start'
            }

            post {
                success {
                    echo 'Application started with PM2'
                }
                failure {
                    error('Failed to start application with PM2')
                }
            }
        }
    }
}
