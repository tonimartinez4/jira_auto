pipeline {
    agent any

    stages {
        stage('HTTP Checks') {
            steps {
                script {
                    def urls = [
                        'https://example.com/api/health1',
                        'https://example.com/api/health2'
                    ]
                    def failed = []

                    urls.each { url ->
                        def code = sh(
                            script: "curl -s -o /dev/null -w \"%{http_code}\" ${url}",
                            returnStdout: true
                        ).trim()
                        echo "Checked ${url} → HTTP ${code}"
                        if (!code.startsWith("2")) {
                            failed << "${url} (code ${code})"
                        }
                    }

                    // Send GitHub status via publishChecks
                    publishChecks(
                        name: 'HTTP Checks',
                        title: 'HTTP Endpoint Checks',
                        summary: failed ? "Failed URLs: ${failed.join(', ')}" : "All URLs OK",
                        status: failed ? 'FAILURE' : 'SUCCESS'
                    )

                    if (failed) {
                        error "Some HTTP checks failed"
                    }
                }
            }
        }
    }
}
