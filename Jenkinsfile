pipeline {
    agent any

    tools {
        nodejs 'Node18'
    triggers {
        cron('H 9 * * *')
    }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Node & NPM') {
            steps {
                bat 'node --version'
                bat 'npm --version'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Install Playwright Browsers') {
            steps {
                bat 'npx playwright install'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                bat 'npx playwright test'
            }
        }
        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                sh 'npx playwright test'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'playwright-report/**', allowEmptyArchive: true
        }
          always {
        emailext(
            to: 'velmurugan@stepladdersolutions.com',
            subject: "Build ${currentBuild.currentResult}",
            body: "Check build: ${BUILD_URL}"
        )
    }
    }
    

}



