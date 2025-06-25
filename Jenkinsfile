pipeline {
    agent any
    parameters {
        booleanParam(name: 'RUN_FRONTEND_TESTS', defaultValue: false, description: 'Run frontend tests?')
    }
    stages {
        stage('Run Tests') {
            parallel {
                stage('Backend Tests') {
                    steps {
                        sh 'node ./backend/test.js'
                    }
                }
                stage('Frontend Tests') {
                    when {
                        expression { params.RUN_FRONTEND_TESTS }
                    }
                    steps {
                        sh 'node ./frontend/test.js'
                    }
                }
            }
        }
        stage('Deploy') {
            when {
                expression { env.GIT_BRANCH == 'origin/main' }
            }
            steps {
                // Input step for manual approval before deployment
                input {
                    message 'Deploy the application?'
                    // You can add an 'id' here for multiple inputs, e.g., id: 'DeployConfirmation'
                    // You can also add 'ok: 'Proceed', submitter: 'admin', submitterParameter: 'approvedBy'
                }
                echo 'Deploying...'
                // Add your actual deployment commands here, e.g.:
                // sh 'npm run deploy'
                // sh 'scp -r build/* user@yourserver:/var/www/html'
            }
        }
    }
}
