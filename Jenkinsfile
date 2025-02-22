pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "my-nodejs-project"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'npm test'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                    sh "docker run -d -p 3000:3000 ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }
    }

    post {
        always {
            script {
                sh 'docker ps -a'
            }
        }
    }
}