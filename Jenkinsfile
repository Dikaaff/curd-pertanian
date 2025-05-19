pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/Dikaaff/curd-pertanian',
                    branch: 'development',
                    credentialsId: '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' // ← GANTI DENGAN ID KREDENSIAL KAMU
                )
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'echo "Installing dependencies..."'
                // sh 'npm install' atau composer install dll
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'echo "Running tests..."'
                // sh 'npm test' atau phpunit dll
            }
        }
    }

    post {
        failure {
            echo '❌ Build Failed'
        }
        success {
            echo '✅ Build Success'
        }
    }
}
