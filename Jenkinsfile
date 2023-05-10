pipeline {
    agent any
        stages {
        stage('Initialize'){
            steps{
                echo "Esta es el inicio"
            }
        }
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
     }
     post {
    always {
      script {
        def slackChannel = '#fundamentos-de-devops'
        def slackMessage = 'Alfredo!!!!!!'
        slackSend (channel: slackChannel, message: slackMessage)
      }
    }
  }
    
    
    
}
