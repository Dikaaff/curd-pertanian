pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'development', url: 'https://github.com/username/repo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'npm test'
            }
        }
    }

    post {
        success {
            echo '✅ Build Passed'
        }
        failure {
            echo '❌ Build Failed'
        }
    }
}
