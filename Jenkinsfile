
pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    set -e
                    echo "Starting pipeline deployment..."

                    rsync -av --delete --exclude='.git/' \
                    "$WORKSPACE/" /var/www/jenkins-auto-deployment/

                    echo "Deployment completed successfully!"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline deployment successful!'
        }
        failure {
            echo 'Pipeline deployment failed!'
        }
    }
}
