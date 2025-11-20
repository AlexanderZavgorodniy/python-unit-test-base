pipeline {
    agent any
    stages {
        stage('Install') {
            steps {
                sh 'python3 -m pip install --user coverage'
            }
        }
        stage('Test + Coverage') {
            steps {
                sh '''
                    python3 -m coverage run -m unittest discover -v
                    python3 -m coverage report
                    python3 -m coverage html
                    python3 -m coverage xml
                '''
            }
            post {
                always {
                    archiveArtifacts artifacts: 'htmlcov/**', allowEmptyArchive: true
                    publishHTML target: [
                        reportDir: 'htmlcov',
                        reportFiles: 'index.html',
                        reportName: 'Coverage Report'
                    ]
                }
            }
        }
    }
}