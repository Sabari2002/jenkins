pipeline {
    agent any  // This will run the pipeline on any available agent

    stages {
        stage('Clone Repository') {
            steps {
<<<<<<< HEAD
                git branch: 'main', url: 'https://github.com/your-repo/my-python-project.git'
=======
                echo 'Cloning the repository...'
                git branch: 'main', url: 'https://github.com/Sabari2002/jenkins'
            }
        }
        stage('Create Virtual Environment') {
            steps {
                echo 'Creating virtual environment...'
                script {
                    docker.image('python:3.11').inside {
                        sh 'python3 -m venv venv'
                    }
                }
>>>>>>> 68a0b2036c97a0d302ecebc55e4c2deb2b5009bc
            }
        }
        stage('Setup Environment') {
            steps {
<<<<<<< HEAD
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
=======
                echo 'Installing dependencies...'
                script {
                    docker.image('python:3.11').inside {
                        sh '. venv/bin/activate && pip install --upgrade pip && pip install -r requirements.txt'
                    }
                }
>>>>>>> 68a0b2036c97a0d302ecebc55e4c2deb2b5009bc
            }
        }
        stage('Run Tests') {
            steps {
<<<<<<< HEAD
                // Run pytest and generate JUnit-compatible test results
                sh './venv/bin/pytest --junitxml=test-results.xml'
=======
                echo 'Running tests...'
                script {
                    docker.image('python:3.11').inside {
                        sh '. venv/bin/activate && pytest --junitxml=results.xml'
                    }
                }
>>>>>>> 68a0b2036c97a0d302ecebc55e4c2deb2b5009bc
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
<<<<<<< HEAD
=======

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
>>>>>>> 68a0b2036c97a0d302ecebc55e4c2deb2b5009bc
}
