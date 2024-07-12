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
        
        stage('Start Application') {
            steps {
                script {
                    // Kill any process running on port 3000
                    sh 'fuser -k 3000/tcp || true'
                    sh 'nohup npm start &'
                }
            }
            
            post {
                success {
                    echo 'Application is up and running and accessible!'
                }
                failure {
                    error('Application failed to start or is not accessible!')
                }
            }
        }
    }
}
