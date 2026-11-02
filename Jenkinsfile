pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t jenkins-cicd-demo .'
            }
        }

        stage('Test Application') {
            steps {
                bat 'docker run --rm jenkins-cicd-demo python -c "import ast; ast.parse(open(\'app.py\').read()); print(\'Test passed\')"'
            }
        }

        stage('Deploy Application') {
            steps {
                bat 'docker rm -f jenkins-cicd-demo 2>NUL & exit /b 0'
                bat 'docker run -d --name jenkins-cicd-demo -p 8082:8000 jenkins-cicd-demo'
            }
        }
    }
}