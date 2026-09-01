pipeline {
    agent any
    environment {
        REGISTRY_URL = 'docker.io' 
        IMAGE_TAG    = "${BUILD_NUMBER}"
        DOCKER_USER = 'haritina'
        DOCKER_IMAGE = 'vue-jenkins-frontend'
        DOCKER_CONTAINER = 'vue-jenkins'
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
                        echo "$DOCKER_ACCESS_TOKEN" | docker login $REGISTRY_URL -u $DOCKER_USER --password-stdin
                        
                        docker compose build frontend
                        
                        docker compose push
                        
                        docker logout $REGISTRY_URL
                    '''
                }
            }
        }
        stage('Deploy') {
            withCredentials([
                sshUserPrivateKey(credentialsId: 'SERVER_SSH_KEY', keyFileVariable: 'SERVER_SSH_KEY'),
                string(credentialsId: 'SERVER_IP', variable: 'SERVER_IP'),
                string(credentialsId: 'SERVER_USER', variable: 'SERVER_USER'),
            ]) {
                sh '''
                    ssh -i \${SERVER_SSH_KEY} -o StrictHostKeyChecking=no \${SERVER_USER}@\${SERVER_IP} "echo 'Connexion réussie !' && uname -a"

                    docker pull $DOCKER_USER/$DOCKER_IMAGE:$DOCKER_TAG

                    docker run -d --name $DOCKER_CONTAINER -p 8080:8080 $DOCKER_USER/$DOCKER_IMAGE:$DOCKER_TAG 
                '''
            }
        }
    }
}