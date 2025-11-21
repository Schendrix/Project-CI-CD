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
        stage('Build/Package') {
            steps {
                // Package your project into a ZIP (excluding .git and Jenkins files)
                sh '''
                zip -r ${ARTIFACT_NAME} . -x "*.git*" "Jenkinsfile"
                '''
            }
        }
        stage('Archive Artifact') {
            steps {
                // Store the artifact in Jenkins
                archiveArtifacts artifacts: "${ARTIFACT_NAME}", fingerprint: true
            }
        }
        stage('build') {
            steps {
                sh 'python3 --version'
                echo "Variable 1 is ${VAR1}"
            }
        }
    }

    post {
        // always {
        //     archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
        //     junit 'build/reports/**/*.xml'
        // }
        always {
            mail to: 'andreisendrea21@gmail.com',
                subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                body: "Something is wrong with ${env.BUILD_URL} and ${ARTIFACT_NAME}"
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo "Artifact created successfully: ${ARTIFACT_NAME}"
            echo 'I succeeded!'
            echo 'Added for webhook'
        }
        // unstable {
        //     echo 'I am unstable :/'
        // }
        // failure {
        //     echo 'I failed :('
        // }
        // changed {
        //     echo 'Things were different before...'
        // }
    }
}