#!/user/bin/env groovy

library identifier: "jenkins-shared-library@master", retriever: modernSCM(
    [$class: 'gitSCMSource',
    remote: 'https://github.com/ILO2003/Module8-SL.git',
    credentialsId: 'github-credentials'])

def gv
pipeline {
    agent any
    tools{
        maven 'maven-3.9'
    }
    stages {
        stage("init"){
            steps{
                script{
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build image and push image") {
            steps {
                script {
                    buildImage 'ilo2003/testing:jma-3.0'
                    dockerLogin()
                    dockerPush 'ilo2003/testing:jma-3.0'
                }
            }
        }
         stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}
