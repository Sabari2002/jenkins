pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git branch: 'main', url: 'https://github.com/Sabari2002/jenkins'
            }
        }
        stage('Install Dependencies') {
            steps {
                echo 'Creating virtual environment and installing dependencies...'
                script {
                    // Create a virtual environment
                    sh 'python3 -m venv venv'

                    // Activate the virtual environment and install dependencies
                    sh '. venv/bin/activate && pip install -r requirements.txt'
                }
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                script {
                    // Activate the virtual environment and run tests
                    sh '. venv/bin/activate && pytest --junitxml=results.xml'
                }
            }
        }
        stage('Publish Test Results') {
            steps {
                echo 'Publishing test results...'
                junit 'results.xml'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs() // Clean up workspace after each run
        }
        success {
            echo 'Pipeline completed successfully.' // Message on successful completion
        }
        failure {
            echo 'Pipeline failed.' // Message if the pipeline fails
        }
    }
}
