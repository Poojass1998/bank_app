pipeline {
    agent any
    environment {
        SERVER_PORT = 9090  // Port for the Python HTTP server
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Example: Place the build logic here, if required.
            }
        }
        stage('Serve HTML Page') {
            steps {
                script {
                    // Stop any existing process running on port 9090
                    sh '''
                    if lsof -t -i:${SERVER_PORT}; then
                        kill -9 $(lsof -t -i:${SERVER_PORT})
                    fi
                    '''

                    // Start the Python HTTP server
                    sh "nohup python3 -m http.server ${SERVER_PORT} --directory . &"
                }
            }
        }
    }
    post {
        always {
            echo 'Build completed.'
        }
    }
}

