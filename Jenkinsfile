pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'karteek0077/eureka-service'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Karteek0077/Eureka-service.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${BUILD_NUMBER}")
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