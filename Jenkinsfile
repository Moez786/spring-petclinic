pipeline {
    agent any
    parameters { choice(name: 'BRANCH_TO_BUILD', choices: ['main', 'REL1'], description: 'Branch options to build'),
                string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'Maven goal to do') }
    triggers { pollSCM("* * * * *") }
    stages {
        stage ("vcs"){
            steps {
                git url: "https://github.com/Moez786/spring-petclinic.git",
                branch: "${params.BRANCH_TO_BUILD}"
            }
        }
         stage ("build") {
            agent {label "OPENJDK11-MVN3.6"}
            steps {
                sh "/usr/share/maven/bin/mvn ${params.MAVEN_GOAL}"
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