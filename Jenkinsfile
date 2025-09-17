pipeline {
    agent any

    stages {
        stage('HTTP Checks') {
            steps {
                script {
                    def urls = ['https://example.com/api/health1']
                    def failed = []

                    urls.each { url ->
                        def code = sh(
                            script: "curl -s -o /dev/null -w \"%{http_code}\" ${url}",
                            returnStdout: true
                        ).trim()
                        echo "Checked ${url} → ${code}"
                        if (!code.startsWith("2")) { failed << url }
                    }

                    if (failed) {
                        error "Failed URLs: ${failed.join(', ')}"
                    }
                }
            }
        }
    }

    post {
        success {
            githubNotify context: 'HTTP Checks', status: 'SUCCESS', description: 'All endpoints OK'
        }
        failure {
            githubNotify context: 'HTTP Checks', status: 'FAILURE', description: 'Some endpoints failed'
        }
    }
}
