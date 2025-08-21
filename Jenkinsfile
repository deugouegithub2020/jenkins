pipeline {
    agent any 

    parameters {
        choice(name: 'VERSION', choices: ['1.2.0', '1.3.0'], description: 'Choose the version to deploy')
    }

    environment {
        DEFAULT_VERSION = "1.3.0"
        SERVER_CREDENTIALS = credentials('github-jenkins-creds')
    }

    stages {
        /* stage("checkout") {
            steps {
                sh 'pwd'
                sh 'ls -ltra'
                sh 'rm -rf serges && mkdir -p serges'
                withCredentials([usernamePassword(
                    credentialsId: 'github-jenkins-creds',
                    usernameVariable: 'GIT_USER',
                    passwordVariable: 'GIT_PASS'
                )]) {
                    sh 'git clone -b dev https://${GIT_USER}:${GIT_PASS}@github.com/deugouegithub2020/jenkins.git serges'
                }
            }
        } */

        stage("checkout") {
            steps {
                sh 'pwd'
                sh 'ls -ltra'
                sh 'rm -rf serges && mkdir -p serges'
                // Use Jenkins built-in git step (cleaner than manual git clone)
                dir('serges') {
                    git branch: 'dev', url: 'https://github.com/deugouegithub2020/jenkins.git', credentialsId: 'github-jenkins-creds'
                }
            }
        }
        

        stage("build") {
            when {
                expression { return env.BRANCH_NAME == 'pr' }
            }
            steps {
                echo "building application"
            }
        }

        stage("test") {
            steps {
                script {
                    echo "We are Testing version ${params.VERSION}"
                    currentBuild.description = "Build #${env.BUILD_NUMBER} - Triggered by Jenkins Pipeline"
                    currentBuild.displayName = "#${env.BUILD_NUMBER}"
                }
            }
        }

        stage("deploy") {
            steps {
                echo "deploying application"
            }
        }
    }

    post {
        always {
            echo "just ran the first pipeline"
        }
        success {
            echo "the build #${env.BUILD_NUMBER} ran successfully."
        }
        failure {
            echo "the pipeline failed"
        }
    }
}
