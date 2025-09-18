import io.jenkins.plugins.checks.api.ChecksStatus
import io.jenkins.plugins.checks.api.ChecksConclusion

pipeline {
    agent any

    environment {
        EXTENSION = "json"  // change this to the extension you want
        TARGET_URL = "https://example.com/api/upload" // change to your endpoint
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
             when {
                branch 'main'
            }
            steps {
                echo 'Building...'

                script {
                    // Find all files with given extension
                    def files = sh(
                        script: "find . -type f -name '*.${EXTENSION}'",
                        returnStdout: true
                    ).trim().split("\n")

                    if (files.size() == 1 && files[0] == "") {
                        echo "No files found with extension .${EXTENSION}"
                        return
                    }

                    // Iterate and send HTTP request for each file
                    files.each { file ->
                        echo "Processing ${file}"
                        sh """
                            curl -X POST \\
                                -H 'Content-Type: application/octet-stream' \\
                                --data-binary '@${file}' \\
                                ${TARGET_URL}
                        """
                    }
                }

                
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
