pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Sabari2002/jenkins'
            }
        }

        stage('Create Virtual Environment and Install Dependencies') {
            steps {
                // Use PowerShell for virtual environment setup and dependency installation
                powershell '''
                python -m venv venv
                .\\venv\\Scripts\\Activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                powershell '''
                .\\venv\\Scripts\\Activate
                python -m unittest discover -s tests
                '''
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'test-results/*.xml'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }

        failure {
            echo 'Pipeline failed.'
        }

        success {
            echo 'Pipeline completed successfully.'
        }
    }
}
