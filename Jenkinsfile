pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "dikaaff/pertanian-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/Dikaaff/curd-pertanian',
                    branch: 'development',
                    credentialsId: 'github-token' // ← Ganti dengan ID kredensial GitHub kamu
                )
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'echo "Installing dependencies..."'
                // sh 'composer install' atau sejenisnya
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'echo "Running tests..."'
                // sh 'vendor/bin/phpunit' atau sejenisnya
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: 'dockerhub-credentials', url: '' ]) {
                    script {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }

    post {
        failure {
            echo '❌ Build or Deployment Failed'
        }
        success {
            echo '✅ CI/CD Pipeline Success! Deployed to Staging.'
        }
    }
}
