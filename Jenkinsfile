def gv 

pipeline {
    agent any
    parameters{
        choice (name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: 'add desc here')
        booleanParam(name: 'executeTests', defaultValue: true, description: ' true or false boolean')
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }

        stage("build") {
            steps {
                script {
                    gv.buildApp()
                }
            }
        }
        stage("test") {
            when {
                expression {
                    params.executeTests 
                }
            }
            steps {
              script {
                    gv.testApp()
                }
            }
        }
         stage("deploy") {
            steps {
                script {
                    gv.buildApp()
                }
            }
        }
    }
}
