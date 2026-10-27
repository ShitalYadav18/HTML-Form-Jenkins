
pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
                echo 'Code fetched from GitHub'
            }
        }

        stage('Test HTML Form') {
            steps {
                script {
                    if (!fileExists('index.html')) {
                        error('index.html file not found')
                    }

                    def html = readFile('index.html')

                    def checks = [
                        '<form',
                        'id="name"',
                        'type="email"',
                        'id="contact"',
                        'type="submit"'
                    ]

                    for (def item : checks) {
                        if (!html.contains(item)) {
                            error("Test failed: ${item} not found")
                        }
                        echo "PASS: ${item} found"
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'All HTML form tests passed!'
        }
        failure {
            echo 'Pipeline or HTML form tests failed.'
        }
    }
}
