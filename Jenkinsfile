pipeline {
    agent any 
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
                    currentBuild.description = "Build #${env.BUILD_NUMBER} - Triggered by Jenkins Pipeline"
                    currentBuild.displayName = "#${env.BUILD_NUMBER} - #${GIT_COMMITTER_NAME"
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
                echo "the build #${env.BUILD_NUMBER} ran successfully. It was committed by #${GIT_COMMITTER_NAME} "
            }
            failure {
                echo "the pipeline failed"
            }
        }
}
