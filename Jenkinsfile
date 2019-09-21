pipeline {
    agent any
    stages {
        stage('Build'){
            steps {
                sh '/Users/karn/DevTools/apache-maven-3.6.2/bin/mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving....'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage ('Deploy to Staging') {
            steps {
                build job: 'deploy-to-staging'
            }
        }
        stage ('Deploy to Production') {
            steps {
                timeout(time:5, until:'DAYs') {
                    input message: 'Approval PRODUCTION Deployment.'
                }
                build job: 'deploy-to-prod'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }
                failure {
                    echo 'Deploy failed.'
                }
            }
        }
    }
}