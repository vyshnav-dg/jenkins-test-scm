pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Checking out code from GitHub...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def imageName = "jenkins-docker-test"
                    echo "🐳 Building Docker image: ${imageName}"
                    bat 'docker rmi jenkins-docker-test || echo "Image not found, skipping removal"'
                    bat 'docker build -t jenkins-docker-test .'

                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    def imageName = "jenkins-docker-test"
                    echo "🚀 Running Docker container..."
                    bat "docker run --rm ${imageName}"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Docker pipeline completed successfully!'
        }
        failure {
            echo '❌ Docker pipeline failed. Check logs for details.'
        }
    }
}
