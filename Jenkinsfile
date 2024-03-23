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
                    env.ENV = input message: "Select the environment to deploy to", ok "Done", parameters: [choice(name: 'ONE', choices: ['dev', 'staging', 'prod'], description: 'Choose between those:')]
                    gv.deployApp()
                    echo "Deploying to ${ENV}"
                }
            }
        }
    }
}
