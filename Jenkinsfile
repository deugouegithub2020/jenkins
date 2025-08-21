pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'dev',
                    url: 'https://github.com/deugouegithub2020/jenkins.git',
                    credentialsId: 'github-jenkins-creds'
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
   
