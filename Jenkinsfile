pipeline {
    agent any

    //triggers {
        //githubPush()
    //}

    stages {
        stage('Run HTTP checks') {
            steps {
                script {
                    // List of URLs to check
                    def urls = [
                        'https://example.com/api/health1',
                        'https://example.com/api/health2'
                    ]

                    def failedUrls = []

                    urls.each { url ->
                        def response = sh(
                            script: "curl -s -o /dev/null -w \"%{http_code}\" ${url}",
                            returnStdout: true
                        ).trim()

                        echo "URL: ${url} returned ${response}"

                        if (!response.startsWith('2')) {
                            failedUrls << url
                        }
                    }

                    if (failedUrls) {
                        error("HTTP check failed for: ${failedUrls.join(', ')}")
                    }
                }
            }
        }
    }
}

