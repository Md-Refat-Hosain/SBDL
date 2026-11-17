pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'pipenv --python python3 sync'
            }
        }
        stage('Test') {
            steps {
                sh 'pipenv run pytest'
            }
        }
        stage('Package') {
            when {
                anyOf { branch "main" ; branch "master" ; branch 'release' }
            }
            steps {
                sh 'python3 -m zipfile -c sbdl.zip lib/'
            }
        }
        stage('Release') {
            when {
                branch 'release'
            }
            steps {
                sh 'echo "Simulating release deployment locally..."'
            }
        }
        stage('Deploy') {
            when {
                anyOf { branch "main" ; branch "master" }
            }
            steps {
                sh 'echo "Simulating production deployment locally..."'
            }
        }
    }
}
