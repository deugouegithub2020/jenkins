pipeline {
    agent any 
    parameters {
        choice: (Name: 'VERSION', choices:['1.2.0' , '1.3.0'], description: 'Choose the version to deploy')
   environment {
        VERSION = "1.3.0"
        SERVER_CREDENTIALS = credentials ('github-jenkins-creds')
    }
    stages {
        stage ("checkout") {
            steps {
                sh 'pwd'
                sh 'ls -ltra'
                sh 'rm -rf serges && mkdir -p serges'
                withCredentials([usernamePassword(credentialsId: 'github-jenkins-creds', 
                                                 usernameVariable: 'GIT_USER', 
                                                 passwordVariable: 'GIT_PASS')]) {
                    sh 'git clone -b dev https://${GIT_USER}:${GIT_PASS}@github.com/deugouegithub2020/jenkins.git serges'
                }
            }
        }
        stage ("build") {
            when {
                expression {
                    BRANCH_NAME == 'pr'
                }
            }
            steps {
                echo "building application"
            }
        }
        stage ("test") {
            steps {
                script {
                    /* echo "Testing with ${SERVER_CREDENTIALS}" */
                    echo "We are Testing version ${params.VERSION}"
                    currentBuild.description = "Build #${env.BUILD_NUMBER} - Triggered by Jenkins Pipeline"
                    currentBuild.displayName = "#${env.BUILD_NUMBER} - #${env.GIT_COMMITTER_NAME}"
                                       
                }
            }
        }        stage ("deploy") {
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
                echo "the build #${env.BUILD_NUMBER} ran successfully. It was committed by #${env.GIT_COMMITTER_NAME}"
            }
            failure {
                echo "the pipeline failed"
            }
        }
}
   
