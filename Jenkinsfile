pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    // Example step
                    sh 'echo "Building..."'
                }
            }
        }
    }
    post {
        success {
            githubNotify context: 'CI/CD', description: 'Build passed', status: 'SUCCESS'
        }
        failure {
            githubNotify context: 'CI/CD', description: 'Build failed', status: 'FAILURE'
        }
