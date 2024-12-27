pipeline {
    agent {
        docker {
            image 'python:3.10-slim'
            args '--user root'
        }
    }
    
    environment {
        PYTHONPATH = '/var/jenkins_home/workspace/my_python_job'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Sabari2002/jenkins.git'
            }
        }
        stage('Setup Environment') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'pytest --junitxml=results.xml' 
            }
        }
    }
    post {
        always {
            junit '**/results.xml'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Investigate the logs.'
        }
    }
}
