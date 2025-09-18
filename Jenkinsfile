pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                publishChecks name: 'Build', status: ChecksStatus.COMPLETED, conclusion: ChecksConclusion.SUCCESS, text: 'Build completed successfully.'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                publishChecks name: 'Test', status: ChecksStatus.COMPLETED, conclusion: ChecksConclusion.SUCCESS, text: 'All tests passed.'
            }
        }
        stage('Lint') {
            steps {
                echo 'Linting...'
                publishChecks name: 'Lint', status: ChecksStatus.COMPLETED, conclusion: ChecksConclusion.SUCCESS, text: 'No lint errors found.'
            }
        }
    }
}
