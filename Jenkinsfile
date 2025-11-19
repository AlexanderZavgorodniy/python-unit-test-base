pipeline {
    agent any
    stages {
        stage('Debug') {
            steps {
                // Проверяем, что мы в нужной директории и файлы на месте
                sh '''
                    echo "Текущая директория: $(pwd)"
                    ls -la
                    cat requirements.txt  # Убираем echo "MISSING", так как файл должен быть
                    python --version
                '''
            }
        }
        stage('Install') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                sh 'python -m pytest'
            }
        }
    }
}
