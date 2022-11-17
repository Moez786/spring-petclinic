pipeline {
    agent any
    triggers { pollSCM("* * * * *") }
    stages {
        stage ("vcs"){
            steps {
                git url: "https://github.com/Moez786/spring-petclinic.git",
                branch: "REL1"
            }
        }
         stage ("build") {
            agent {label "OPENJDK11-MVN3.6"}
            steps {
                sh "/usr/share/maven/bin/mvn package"
            }
         }
         stage ("Junit") {
            agent {label "OPENJDK11-MVN3.6"}
            steps {
                junit "**/surefire-reports/*.xml"
            }
         }
    }
}