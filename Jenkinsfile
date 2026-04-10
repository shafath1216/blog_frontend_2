pipeline {
    agent any

    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Deploy') {
            steps {
                script {
                    // Match the backend logic: use the frontend specific folder
                    dir('/opt/blog-project/blog-frontend') {

                        // Pull the code
                        checkout scm

                        // Run docker-compose referencing the parent directory
                        // Target the 'frontend' service specifically
                        sh 'docker-compose -f ../docker-compose.yml up -d --build frontend'
                        sh 'docker image prune -f'
                    }
                }
            }
        }
    }

    post {
        success { echo '✅ Frontend Deployment complete!' }
        failure { echo '❌ Frontend still hitting a wall. Check console output.' }
    }
}
