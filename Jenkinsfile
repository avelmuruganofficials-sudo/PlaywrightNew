pipeline {
    agent any

    triggers {
        cron('H 9 * * *')   // runs daily around 9 AM
    }
    tools {
    nodejs 'nodejs'
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
    }

    post {
        always {
            echo 'Pipeline finished'
        }

        success {
            emailext(
                to: 'velmurugan@stepladdersolutions.com',
                subject: '✅ Jenkins Playwright Build SUCCESS',
                body: """
                Build Successful!

                Job: ${JOB_NAME}
                Build Number: ${BUILD_NUMBER}
                URL: ${BUILD_URL}
                """
            )
        }

        failure {
            emailext(
                to: 'velmurugan@stepladdersolutions.com',
                subject: 'Jenkins Playwright Build FAILED',
                body: """
                Build Failed!

                Job: ${JOB_NAME}
                Build Number: ${BUILD_NUMBER}
                Check logs: ${BUILD_URL}
                """
            )
        }
    }
}


