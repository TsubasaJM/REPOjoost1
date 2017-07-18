pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'chmod +x flakey-deploy.sh health-check.sh'
            }
        }
        stage('Deploy') {
            steps {
                retry(3) {
                    sh './flakey-deploy.sh'
                }
            }
        }
        stage('Health check') {
            steps {
                timeout(time: 8, unit: 'SECONDS') {
                    sh './health-check.sh'
                }
            }
        }
    }
}
