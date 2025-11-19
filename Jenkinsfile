pipeline {
    agent any
    stages {
        stage('Debug') {
            steps {
                // Явно клонируем — обходим все проблемы с checkout scm
                sh '''
                    git clone https://github.com/AlexanderZavgorodniy/python-unit-test-base.git .
                    ls -la
                    cat requirements.txt || echo "⚠️ requirements.txt MISSING"
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