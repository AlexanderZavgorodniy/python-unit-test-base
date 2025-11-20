pipeline {
    agent { docker 'python:3.12-slim' }

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
                    coverage xml
                '''
            }
        }
    }

    post {
        always {
            // Сохраняем HTML-отчёт как артефакт (доступен в "Artifacts")
            archiveArtifacts artifacts: 'htmlcov/**', allowEmptyArchive: true
            // coverage.xml тоже можно сохранить, если нужно:
            // archiveArtifacts artifacts: 'coverage.xml'
        }
    }
}
