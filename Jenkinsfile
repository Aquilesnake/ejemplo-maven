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
                stage('unit') {
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
                stage('run') {
                    steps {
                        sleep 20
                        dir('C:\\Users\\AKLSNK\\Desktop\\clases DevOps\\Develoment\\Jenkinsfile\\ejemplo-maven'){
                               bat 'start mvnw.cmd spring-boot:run'
                        }
                    }
                }
               stage('test') {
                    steps {
                         dir('C:\\Users\\AKLSNK\\Desktop\\clases DevOps\\Develoment\\Jenkinsfile\\ejemplo-maven'){
                             sleep 20
                               bat 'curl -X GET "http://localhost:8081/rest/mscovid/test?msg=testing"'
                        }
                    }
                }
    }
}
