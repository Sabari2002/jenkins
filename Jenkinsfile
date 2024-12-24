pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Checking out the repository...'
                git url: 'https://github.com/Sabari2002/jenkins', branch: 'main'
            }
        }

        stage('Create Virtual Environment') {
            steps {
                echo 'Creating virtual environment...'
                sh 'python3 -m venv venv'  // Creates a virtual environment
                sh 'source venv/bin/activate'  // Activates the virtual environment
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'source venv/bin/activate && pip install -r requirements.txt'  // Install dependencies in the virtual environment
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'source venv/bin/activate && pytest --junitxml=results.xml'  // Run tests in the virtual environment
            }
        }

        stage('Publish Test Results') {
            steps {
                echo 'Publishing test results...'
                junit 'results.xml'  // Publish test results
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()  // Clean up the workspace
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
