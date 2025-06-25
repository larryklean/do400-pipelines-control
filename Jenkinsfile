pipeline {
    agent any // Or specify a specific agent, e.g., agent { docker 'node:16-alpine' }
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
                echo 'Step not executed...'
                // Add your deployment commands here, e.g.:
                // sh 'npm run deploy'
                // sh 'scp -r build/* user@yourserver:/var/www/html'
            }
        }
    }
}
