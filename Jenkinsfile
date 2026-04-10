pipeline {
    agent any
    
    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Deploy Frontend') {
            steps {
                script {
                    // Navigate to the frontend's specific directory
                    dir('/opt/blog-project/blog-frontend') {
                        
                        // 1. Force a clean checkout to avoid .git/config.lock issues
                        sh 'git clean -fd'
                        checkout scm
                        
                        // 2. Run the build from the root context
                        // We use the hyphenated 'docker-compose' because of the global link we made
                        sh 'cd .. && docker-compose up -d --build frontend'
                        
                        // 3. Clean up dangling images to save disk space
                        sh 'docker image prune -f'
                    }
                }
            }
        }
    }

    post {
        success { echo '🚀 Frontend is live!' }
        failure { echo '💔 Frontend deployment failed. Check the logs.' }
    }
}
