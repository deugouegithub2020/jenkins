pipeline {
    agent any 
    environment {
        VERSION = "1.3.0"
    }
    stages {
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
                    echo "Testing application"
                    echo "We are Testing version ${VERSION}"
                    currentBuild.description = "Build #${env.BUILD_NUMBER} - Triggered by Jenkins Pipeline"
                    currentBuild.displayName = "#${env.BUILD_NUMBER} - #${env.GIT_COMMITTER_NAME}"
                }
            }
        }
        stage ("deploy") {
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
