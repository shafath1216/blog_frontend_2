pipeline {
    agent any
    
    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Deploy Frontend') {
            steps {
                script {
                    // Just "visit" the frontend folder
                    dir('/opt/blog-project/blog-frontend') {
                        
                        // Pull frontend code
                        checkout scm
                        
                        // Move to parent to run compose for the specific service
                        dir('..') {
                            sh 'docker-compose up -d --build frontend'
                            sh 'docker image prune -f'
                        }
                    }
                }
            }
        }
    }

    post {
        success { echo '🚀 Frontend is live!' }
        failure { echo '❌ Frontend deployment failed.' }
    }
}
