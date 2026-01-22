pipeline {
    agent {
        docker {
            //image with playwright and chromium browser
            // image 'playwright/chromium:playwright-1.56.1'
            image 'mcr.microsoft.com/playwright:v1.57.0-noble'
            //permit the container to run as root user
            args '--user=root --entrypoint=""'
        }
    }
    parameters {
       choice(name: 'Navigateur', choices: ['chromium', 'webkit', 'firefox'], description: 'Select the environment to deploy to')
    }

    stages {
        stage('Display versions') {
            steps {
                //display node and npm versions
                sh 'node --version'
                //display npm version
                sh 'npm --version'
                sh'git --version'
            }
        }
        stage(" CLONE DU PROJET"){
            steps{
                //install git
                sh 'apt-get update && apt-get install -y git'
                //remove repo folder if exists
                sh "rm -rf repo"
                //clone the repo
                echo 'version du git'
                sh 'git --version'
                //clone the repo
                sh "git clone https://github.com/admanehocine/PlaywrightJenkins.git repo"
                //list files
                sh "ls -la repo"
            
                //list files in current directory
                  dir('repo'){
                    //install dependencies and run tests
                    //install playwright browsers
                    sh "npm ci"
                    //run tests with chromium
                    script {
                        if (params.Navigateur == 'chromium') {
                            sh "npx playwright test --project=chromium"
                        } else{
                            if (params.Navigateur == 'firefox') {
                                sh "npx playwright test --project=firefox"
                            } else {
                                sh "npx playwright test --project=webkit"
                            }
                        }
                    }   
                    sh "npx playwright test --project=chromium"
                }
            }
        }
        
      
    }
   
}