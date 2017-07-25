pipeline {
    agent any
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }
    stages {
        stage('Build') {
            steps {
                sh 'chmod +x flakey-deploy.sh health-check.sh'
            }
        }
        stage('Deploy') {
            steps {
                retry(3) {
                    // sh './flakey-deploy.sh'
                    sh 'printenv'
                }
            }
        }
        stage('Health check') {
            steps {
                timeout(time: 10, unit: 'SECONDS') {
                    sh './health-check.sh'
                }
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
