/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
    environment {
        CONTROL = 'true'
        VAR1 = 'var1'
    }
    stages {
        stage('initialize') {
            steps {
                sh 'sudo apt-get install -y python3'
                echo "Control var is ${CONTROL}"
            }
        }
        stage('build') {
            steps {
                sh 'python3 --version'
                echo "Variable 1 is ${VAR1}"
            }
        }
        // stage('Build2') {
        //     steps {
        //         sh './gradlew build'
        //     }
        // }
        // stage('Test') {
        //     steps {
        //         sh './gradlew check'
        //     }
        // }
    }

    post {
        // always {
        //     archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
        //     junit 'build/reports/**/*.xml'
        // }
        always {
            mail to: 'andreisendrea21@gmail.com',
                subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                body: "Something is wrong with ${env.BUILD_URL}"
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
}