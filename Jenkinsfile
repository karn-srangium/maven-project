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
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging') {
            steps {
                build job: 'deploy-to-staging'
            }
        }
    }
}