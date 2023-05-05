pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
        post {
            always {
                slackSend channel: 'fundamentos-de-devops', color: '#33B5FF', message: 'Prueba de Nuevo Mensaje', teamDomain: 'sustantivagrupo', tokenCredentialId: '7645404f-1a5f-42d1-93e6-6b65f095d628', username: 'AlfredoCrDev'
            }
            failure {
                slackSend "Build failed  - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            }
        }
    }
}
