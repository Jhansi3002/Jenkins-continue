pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-python-app .'
            }
        }

        stage('Stop Old Container') {
    steps {
        sh '''
          docker-compose down --remove-orphans || true
        '''
    }
}


        stage('Deploy Application (CD)') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        success {
            echo "✅ Application deployed successfully!"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
