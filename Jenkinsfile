/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
    stages {
        stage('initialize') {
            steps {
                sh 'sudo apt-get install -y python'
            }
        }
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
    }
}