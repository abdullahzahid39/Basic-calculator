pipeline {
    agent any
    
    environment {
        // Define the Node.js and npm versions if needed
        NODEJS_HOME = tool name: 'NodeJS', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your GitHub repository
                git 'https://github.com/abdullahzahid39/Basic-calculator.git'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies
                sh 'npm install'
            }
        }
        
        stage('Start Application') {
            steps {
                // Start your Node.js application
                sh 'nohup npm start &'
            }
            
            post {
                success {
                    echo 'Application is up and running!'
                }
                failure {
                    echo 'Failed to start the application!'
                    // Add additional actions upon failure if needed
                }
            }
        }
    }
}
