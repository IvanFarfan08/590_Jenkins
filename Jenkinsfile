pipeline {
    agent {
        docker {
            image 'python:3.12-slim'
            args '-u root'
        }
    }

    stages {
        stage('Install dependencies') {
            steps {
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
