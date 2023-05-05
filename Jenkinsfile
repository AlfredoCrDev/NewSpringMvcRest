pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B package'
            }
        }
        stage('Test') {
            steps {
                sh "mvn clean verify"
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
        }
    }
}
