pipeline {
    agent { docker 'python:3.12-slim' }

    stages {
        stage('Install') {
            steps {
                sh 'pip install coverage'
            }
        }

        stage('Test + Coverage') {
            steps {
                sh '''
                    # Запуск всех тестов через unittest с покрытием
                    coverage run -m unittest discover -v

                    # Отчёт в консоль (виден в логе Jenkins)
                    coverage report

                    # Генерация HTML-отчёта
                    coverage html

                    # Генерация XML-отчёта для интеграции (Cobertura)
                    coverage xml
                '''
            }
        }
    }

    post {
        always {
            // Сохранить HTML-отчёт как артефакт
            archiveArtifacts artifacts: 'htmlcov/**', allowEmptyArchive: true

            // Опционально: опубликовать отчёт в UI Jenkins (требует плагин "HTML Publisher")
            publishHTML target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'htmlcov',
                reportFiles: 'index.html',
                reportName: 'Coverage Report'
            ]
        }
    }
}
