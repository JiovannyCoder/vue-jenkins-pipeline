pipeline {
    agent any
    environment {
        REGISTRY_URL = 'docker.io' 
        IMAGE_TAG    = "${BUILD_NUMBER}"
        DOCKER_USER = 'haritina'
    }
    stages {
        stage('Dependencies') {
            steps {
                sh "npm ci"
            }
        }
        stage('Build') {
            steps {
                sh "npm run build"
            }
        }
        stage('Package : docker image & push') {
            steps {
                withCredentials([
                    string(credentialsId: 'DOCKER_ACCESS_TOKEN', variable: 'DOCKER_ACCESS_TOKEN')
                ]) {
                    sh '''
                        echo "$DOCKER_ACCESS_TOKEN" | docker login -u $DOCKER_USER --password-stdin
                        
                        docker compose up frontend
                        
                        docker compose push frontend
                        
                        docker logout
                    '''
                }
            }
        }
    }
}