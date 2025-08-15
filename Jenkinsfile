pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'jenkins', url: 'https://github.com/aharpathi/odoo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building Odoo dependencies..."'
                // Example: install Python deps
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running Odoo tests..."'
                // Example test command
                sh './odoo-bin --test-enable --stop-after-init'
            }
        }

        stage('Store Artifact') {
            steps {
                sh 'echo "Packaging Odoo for deployment..."'
                sh 'tar czf odoo_build.tar.gz .'
                archiveArtifacts artifacts: 'odoo_build.tar.gz', fingerprint: true
            }
        }

        stage('Deploy to Staging') {
            steps {
                sh 'echo "Deploying to staging..."'
                // Deployment script here
            }
        }

        stage('Approval') {
            steps {
                input message: 'Approve deployment to production?'
            }
        }

        stage('Deploy to Production') {
            steps {
                sh 'echo "Deploying to production..."'
                // Production deployment script here
            }
        }
    }
}
