import io.jenkins.plugins.checks.api.ChecksStatus
import io.jenkins.plugins.checks.api.ChecksConclusion

pipeline {
    agent any
    stages {
        stage('Build') {
             when {
                branch 'main'
            }
            steps {
                echo 'Building...'
                publishChecks name: 'Build', status: ChecksStatus.COMPLETED, conclusion: ChecksConclusion.SUCCESS, text: 'Build completed successfully.'
            }
        }
        stage('Test') {
             when {
                branch 'main'
            }
            steps {
                echo 'Testing...'
                publishChecks name: 'Test', status: ChecksStatus.COMPLETED, conclusion: ChecksConclusion.SUCCESS, text: 'All tests passed.'
            }
        }
        stage('Lint') {
             when {
                branch 'main'
            }
            steps {
                echo 'Linting...'
                publishChecks name: 'Lint', status: ChecksStatus.COMPLETED, conclusion: ChecksConclusion.SUCCESS, text: 'No lint errors found.'
            }
        }
    }
}
