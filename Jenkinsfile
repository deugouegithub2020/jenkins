pipeline {
    agent any 
    stages {
        stage ("build") {
            steps {
                echo 'testing application'
            }
        }
        stage ("test") {
            steps {
                echo 'Testing application'
            }
        }
        stage ("deploy") {
            steps {
                echo 'Testing application'
            }
        }
        post {
            always {
                echo 'just ran the first pipeline'
            }
            success {
                echo 'the pipeline ran successfully'
            }
            failure {
                echo 'the pipeline failed'
            }
        }
   }
}
