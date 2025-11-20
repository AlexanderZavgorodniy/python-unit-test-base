pipeline {
    agent any
    stages {
        stage('Debug') {
            steps {
                sh '''
                    echo "Текущая директория: $(pwd)"
                    ls -la
                    echo "Содержимое requirements.txt:"
                    cat requirements.txt
                    echo "Python версия:"
                    python3 --version
                    echo "Pip версия:"
                    pip3 --version
                '''
            }
        }
        stage('Install') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }
    }
}
