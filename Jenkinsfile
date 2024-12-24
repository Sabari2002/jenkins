pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git branch: 'main', url: 'https://github.com/Sabari2002/jenkins'
            }
        }
        stage('Install pipx and Virtual Environment') {
            steps {
                echo 'Installing pipx and creating virtual environment...'
                sh 'pip install --user pipx && pipx ensurepath'
                sh 'pipx install python3.11'
                sh 'pipx run python3 -m venv venv'
            }
        }
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh '. venv/bin/activate && pip install --upgrade pip && pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh '. venv/bin/activate && pytest --junitxml=results.xml'
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
