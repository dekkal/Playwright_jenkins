pipline{

     agent {
        docker {
            image 'playwright/chromium:playwright-1.56.1'
           args '--user=root --entrypoint=""'
        }
       }

stages{
    stage('Démarrage du configuration projet'){
        steps{
            sh 'rm -rf repo'
           }
        steps{
            sh "git clone https://github.com/dekkal/Playwright_jenkins.git repo"
             }
    steps{
        //check version node et playwright
        sh ' echo node -v && npx playwright --version'
    }


        steps{
            //Accéder au dossier du projet
            dir('repo'){
                //Installer les dépendances du projet
                sh 'npm install'      
                sh 'npx playwright test --project=chromium'   

            }

                                                }

     
}
}