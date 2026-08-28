pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                echo "Stage 1 : building"
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Testing"'
                echo "Stage 2 : deploy"
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo "Deploy here bru"'
                echo "Stage 3 : deploy"
            }
        }
    }
}