pipeline {
   agent any
   stages {  
               stage('compiled') {
                   steps {
                       dir('C:\\Users\\AKLSNK\\Desktop\\clases DevOps\\Develoment\\Jenkinsfile\\ejemplo-maven'){
                                   bat './mvnw.cmd clean compile -e'
                           }
                       }
               }
               stage('test') {
                   steps {
                       sleep 10
                       dir('C:\\Users\\AKLSNK\\Desktop\\clases DevOps\\Develoment\\Jenkinsfile\\ejemplo-maven'){
                          bat './mvnw.cmd clean test -e'
                       }
                   }
               }
               stage('jar') {
                   steps {
                       sleep 10
                        dir('C:\\Users\\AKLSNK\\Desktop\\clases DevOps\\Develoment\\Jenkinsfile\\ejemplo-maven'){
                              bat './mvnw.cmd clean package -e'
                       }
                   }
               }
               stage('sonar') {
                   steps {
                       sleep 20
                       dir('C:\\Users\\AKLSNK\\Desktop\\clases DevOps\\Develoment\\Jenkinsfile\\ejemplo-maven'){
                              mvn sonar:sonar -Dsonar.projectKey=ejemplo-mavenSonar  -Dsonar.host.url=http://localhost:9000 -Dsonar.login=4b9f805bfab90cf85026813addfdbd444df39cd7
                       }
                   }
               }
        stage("Nexus_Upload") {
            steps {
                script {
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: '3',
                            protocol: 'https',
                            nexusUrl: 'https://4a172c435d05.ngrok.io/',
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: 'test-nexus',
                            credentialsId: 'nexus-remoto',
                            artifacts: [
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** Archivo: ${artifactPath}, no existe";
                    }
                }
            }
        }
               }
   }
}

