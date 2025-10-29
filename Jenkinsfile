pipeline {
    agent any

    stages {
	stage('Initialize'){
	    def dockerHome = tool 'myDocker'
	    env.PATH = "${dockerHome}/bin:${env.PATH}"
	}
        stage('Install dependencies') {
            steps {
                sh 'python3 -m venv venv'
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
