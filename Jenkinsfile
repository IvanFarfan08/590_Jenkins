pipeline {
    agent {
        docker {
            image 'python:3.12-slim'   // has python3, pip, venv, pytest (after install)
            // If your Jenkins image lacks the Docker CLI, install it or remove args below.
            args '-u root'             // optional: run as root inside the build container
        }
    }

    stages {
        stage('Install dependencies') {
            steps {
                // inside the python:3.12 container
                sh 'python -m venv venv'
                sh './venv/bin/pip install --upgrade pip'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Run tests') {
            steps {
                sh './venv/bin/pytest --junitxml=report.xml'
            }
        }

        stage('Publish Report') {
            steps {
                junit 'report.xml'
            }
        }
    }
}
