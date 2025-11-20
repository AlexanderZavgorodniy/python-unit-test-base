pipeline {
    agent {
        docker {
            image 'python:3.12-slim'
            args '-u root'
        }
    }

    stages {
        stage('Install') {
            steps {
                sh 'pip install --no-cache-dir coverage'
            }
        }

        stage('Test + Coverage') {
            steps {
                sh '''
                    coverage run -m unittest discover -v
                    coverage report
                    coverage html
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'htmlcov/**', allowEmptyArchive: true
        }
    }
}
