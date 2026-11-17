pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Ensure python3/pip are used if pipenv isn't in the container
               sh 'python3 -m venv venv'
               sh './venv/bin/pip install --upgrade pip'
            }
        }
        stage('Test') {
            steps {
                // Use pytest directly if pipenv isn't configured in container
                sh './venv/bin/pytest'
            }
        }
        stage('Package') {
            when {
                anyOf { branch "main" ; branch "master" ; branch 'release' }
            }
            steps {
                // Using python to zip folder if 'zip' utility is missing in Docker
                sh 'python3 -m zipfile -c sbdl.zip lib/'
            }
        }
        stage('Release') {
            when {
                branch 'release'
            }
            steps {
                // Local simulation instead of Prashant's private Azure VM
                sh 'echo "Simulating release deployment locally on Mac..."'
            }
        }
        stage('Deploy') {
            when {
                anyOf { branch "main" ; branch "master" }
            }
            steps {
                // Local simulation instead of Prashant's private Azure VM
                sh 'echo "Simulating production deployment locally on Mac..."'
            }
        }
    }
}
