pipeline {
    agent any

    tools {
        maven 'Maven-3.9'
        jdk 'JDK-17'
    }

    environment {
        DOCKER_REGISTRY = 'docker.io/karteek0077'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Karteek0077/Eureka-service.git',
                    credentialsId: 'github-credentials'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
                junit '**/target/surefire-reports/*.xml'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_REGISTRY}/eureka-service:${BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.image("${DOCKER_REGISTRY}/eureka-service:${BUILD_NUMBER}").push()
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'Eureka Service built successfully!'
        }
        failure {
            mail to: 'your-email@example.com',
                 subject: "Build Failed: Eureka-service - ${currentBuild.fullDisplayName}",
                 body: "Check Jenkins: ${BUILD_URL}"
        }
    }
}
