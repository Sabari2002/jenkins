pipeline {
    agent {
        docker {
            image 'python:3.10-slim'
            args '--user root'
        }
    }
    
    environment {
        PYTHONPATH = '/var/jenkins_home/workspace/my_python_job'
        APP_PORT = '80'
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
        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t myapp:latest .
                docker run -d --name myapp_container -p ${APP_PORT}:${APP_PORT} myapp:latest
                sleep 5
                curl --fail http://localhost:${APP_PORT} || (echo "App failed to start" && exit 1)
                '''
            }
        }
    }
    post {
        always {
            junit '**/results.xml'
            sh 'docker rm -f myapp_container || true'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Investigate the logs.'
        }
    }
}
