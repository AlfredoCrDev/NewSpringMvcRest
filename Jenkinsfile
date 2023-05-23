pipeline {
    agent any
        stages {
          stage('Build') {
            steps { 
                sh 'mvn -B package'
                sh 'mvn clean install'
            }
        }
        stage('SonarQube analysis') {
             environment {
                SCANNER_HOME = tool 'SonarQube Conexion'
            }
            steps {
              withSonarQubeEnv(credentialsId: 'SonarCnx', installationName: 'SonarInDocker') {
              sh '''$SCANNER_HOME/bin/sonar-scanner \
            -Dsonar.projectKey=devopapp \
            -Dsonar.projectName=devopapp \
            -Dsonar.sources=./ \
            -Dsonar.java.binaries=target/classes/ \
            -Dsonar.exclusions=src/test/java/****/*.java \
            -Dsonar.projectVersion=${BUILD_NUMBER}-${GIT_COMMIT_SHORT}'''
             }
            }
        }
        stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    def pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: "nexus2",
                            protocol: "http",
                            nexusUrl: "192.168.1.176:8081/repository/devops/",
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: "repomvndevops",
                            credentialsId: "nexusCredencial",
                            artifacts: [
                                [artifactId: pom.artifactId,
                                        classifier: '',
                                        file: artifactPath,
                                        type: pom.packaging]
                           ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
            }
     }

post {
    failure {
        slackSend(channel: "#fundamentos-de-devops", token: "tokenslack", message: "La ejecución del Pipeline ${BUILD_NUMBER} ha finalizado con estado ${currentBuild.result}, mas informacion en ${RUN_DISPLAY_URL} ")
    }
}

}
