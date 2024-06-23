pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'vishalch32'  // Docker Hub username or registry name
        DOCKER_IMAGE = 'myimage'
        DOCKER_TAG = '1.0'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://your-repository-url.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_REGISTRY}/${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image("${DOCKER_REGISTRY}/${DOCKER_IMAGE}:${DOCKER_TAG}").push()
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
