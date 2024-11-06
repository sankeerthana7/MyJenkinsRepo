pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from SCM
                git url: 'https://github.com/MyJenkinsRepo', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Example for Node.js: Install dependencies
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                sh 'npm test'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy to a test/staging server
                // You can define deployment scripts or use SSH to deploy to remote servers
                sh 'echo "Deploying..."'
            }
        }
    }

    post {
        always {
            // Clean up after every build
            deleteDir()
        }
        success {
            // Actions on success
            echo 'Build and deployment successful!'
        }
        failure {
            // Actions on failure
            echo 'Build failed!'
        }
    }
}
