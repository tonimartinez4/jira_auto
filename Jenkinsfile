pipeline {
    agent any

    stages {
        stage('HTTP Checks') {
            steps {
                commitStatus(context: 'HTTP Checks') {
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
                            echo "Checked ${url} → ${code}"
                            if (!code.startsWith("2")) {
                                failed << "${url} (code ${code})"
                            }
                        }
                        if (failed) {
                            error "Failed URLs: ${failed.join(', ')}"
                        }
                    }
                }
            }
        }
    }
}
