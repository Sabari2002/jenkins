pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git branch: 'main', url: 'https://github.com/Sabari2002/jenkins.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh '''
                python3 -m venv venv  # Create a virtual environment
                source venv/bin/activate  # Activate the virtual environment
                pip install --upgrade pip  # Upgrade pip
                pip install -r requirements.txt  # Install dependencies
                '''
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh '''
                source venv/bin/activate  # Activate the virtual environment
                pytest --junitxml=results.xml  # Run tests
                '''
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
