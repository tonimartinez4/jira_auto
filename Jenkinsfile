pipeline {
    agent any
    stages {
        stage('Build') { steps { echo 'Building...' } }
        stage('Test') { steps { echo 'Testing...' } }
        stage('Deploy') { steps { echo 'Deploying...' } }
    }
    post {
        always {
            // Send build status to GitHub
            githubNotify context: 'Jenkins CI', status: currentBuild.currentResult
        }
    }
}
