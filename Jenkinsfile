pipeline {
    agent {
        docker {
            image 'ubuntu:20.04' // A Docker image with sudo and basic tools
            args '-u root' // Running as root to install dependencies
        }
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git branch: 'main', url: 'https://github.com/Sabari2002/jenkins'
            }
        }
        stage('Install Dependencies') {
            steps {
                echo 'Installing python3-venv and creating virtual environment...'
                script {
                    // Install python3-venv package
                    sh 'apt-get update && apt-get install -y python3.11-venv'

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
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
