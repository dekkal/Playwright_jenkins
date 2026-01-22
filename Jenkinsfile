pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/playwright:v1.57.0-noble'
            args '--user=root --entrypoint=""'
        }
    }

    parameters {
        choice(
            name: 'Navigateur',
            choices: ['chromium', 'webkit', 'firefox'],
            description: 'Choisir le navigateur'
        )

        choice(
            name: 'TAGS',
            choices: ['@valid', '@addedToCart', '@test'],
            description: 'Choisir le tag Playwright'
        )
    }

    stages {

        stage('Display versions') {
            steps {
                sh '''
                    node --version
                    npm --version
                    git --version
                '''
            }
        }

        stage('Clone project') {
            steps {
                sh 'rm -rf repo'
                sh 'git clone https://github.com/admanehocine/PlaywrightJenkins.git repo'
            }
        }

        stage('Install & Run Playwright') {
            steps {
                dir('repo') {
                    sh 'npm ci'

                    sh """
                        echo "Navigateur : ${params.Navigateur}"
                        echo "Tags : ${params.TAGS}"

                        npx playwright test \
                          --project=${params.Navigateur} \
                          --grep "${params.TAGS}"
                    """
                }
            }
        }
    }

    post {
        success {
            echo ' Pipeline SUCCESS'

            script {
                if (params.TAGS == '@test') {
                    echo 'Déclenchement des tests de régression'
                    build job: 'jobRégression'
                }
            }
        }

        
    }
}
