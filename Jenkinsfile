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
                // Ensure any previously running instances are stopped
                sh 'pkill node || true'
                // Start your Node.js application
                sh 'nohup npm start &'
            }
            
            post {
                success {
                    echo 'Application is up and running!'
                    // Optionally verify the application is running by making a request
                    script {
                        def response = sh(script: 'curl -s -o /dev/null -w "%{http_code}" http://localhost:3000', returnStdout: true).trim()
                        if (response == '200') {
                            echo 'Application is accessible at http://localhost:3000'
                        } else {
                            error('Application is not accessible')
                        }
                    }
                }
                failure {
                    echo 'Failed to start the application!'
                }
            }
        }
    }
}
