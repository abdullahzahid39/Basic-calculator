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
                    script {
                        def responseCode = sh(script: "curl -s -o /dev/null -w '%{http_code}' http://localhost:3000", returnStdout: true).trim()
                        if (responseCode == '200') {
                            echo 'Application is up and running and accessible!'
                        } else {
                            error('Application failed to start or is not accessible!')
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
