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
            success {
                slackSend channel: '#fundamentos-de-devops', color: '#6EAB00', message: 'Hasta que por Fin Funciono xD ', teamDomain: 'sustantivagrupo', tokenCredentialId: 'SecretSlack', username: 'Alfredo'
            }
            failure {
                slackSend "Build failed  - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            }
        }
    }
}
