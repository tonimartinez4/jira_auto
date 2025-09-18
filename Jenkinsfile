pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                publishChecks name: 'Build', status: 'completed', conclusion: 'success', output: [title: 'Build', summary: 'Build completed.']
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                publishChecks name: 'Test', status: 'completed', conclusion: 'success', output: [title: 'Test', summary: 'Tests passed.']
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                publishChecks name: 'Deploy', status: 'completed', conclusion: 'success', output: [title: 'Deploy', summary: 'Deployed.']
            }
        }
    }
}
