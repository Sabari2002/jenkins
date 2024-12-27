pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/my-python-project.git'
            }
        }
        stage('Setup Environment') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                // Run pytest and generate JUnit-compatible test results
                sh './venv/bin/pytest --junitxml=test-results.xml'
            }
        }
        stage('Publish Test Results') {
            steps {
                // Publish the test results to Jenkins
                junit 'test-results.xml'
            }
        }
        stage('Run Application') {
            steps {
                sh './venv/bin/python main.py'
            }
        }
    }
}
