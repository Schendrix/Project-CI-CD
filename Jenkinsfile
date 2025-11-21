/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
    stages {
        stage('initialize') {
            steps {
                sh 'sudo apt-get install -y python3'
            }
        }
        stage('build') {
            steps {
                sh 'python3 --version'
            }
        }
    }
}