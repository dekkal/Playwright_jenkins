pipeline {

    agent {
        docker {
            image 'playwright/chromium:playwright-1.56.1'
            args '--user=root --entrypoint=""'
        }
    }

    stages {

        stage('Configuration du projet') {
            steps {

                // Nettoyage
                sh 'rm -rf repo'

                // Clonage du dépôt
                sh 'git clone https://github.com/dekkal/Playwright_jenkins.git repo'

                // Vérification des versions
                sh 'node -v'
                sh 'npx playwright --version'

                // Accès au projet
                dir('repo') {
                    sh 'npm install'
                    sh 'npx playwright test --project=chromium'
                }
            }
        }
    }
}
