pipeline {

    agent {
        docker {
            image 'playwright/chromium:playwright-1.56.1'
            args '--user=root --entrypoint=""'
        }
    }

    stages {

        stage('Vérification versions') {
            steps {
                sh 'node -v'
                sh 'npx playwright --version'
            }
        }

        stage('Install & Run tests') {
            steps {
                sh 'npm install'
                sh 'npx playwright test --project=chromium'
            }
        }
    }
}
