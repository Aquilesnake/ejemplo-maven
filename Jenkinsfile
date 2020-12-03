
pipeline {
    agent any

    stages {   
                stage('compiled') {
                    steps {
                        
                                    bat './mvnw.cmd clean compile -e'
                        }
                }
                stage('unit') {
                    steps {
                        sleep 10
                        
                               bat './mvnw.cmd clean test -e'                       
                    }
                }
                stage('jar') {
                    steps {
                        sleep 10
                   
                               bat './mvnw.cmd clean package -e'
                        
                    }
                }
                    stage('SonarQube analysis') {
                        steps {
                                script{
                        withSonarQubeEnv('sonar'){
                        bat 'mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                            }
                        }
                    }
                }

                stage('run') {
                    steps {
                        sleep 20
                       
                               bat 'start mvnw.cmd spring-boot:run'
                        
                    }
                }
               stage('test') {
                    steps {
                        
                             sleep 20
                               bat 'curl -X GET "http://localhost:8081/rest/mscovid/test?msg=testing"'
                        
                    }
                }
        
        
    }
}
