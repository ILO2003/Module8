pipeline {
    agent any
    parameters{
        string (name: 'SOMETHING', defaultValue: 'some value', description: 'version to deploy on prod') // we are not using this in the example
        choice (name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: 'add desc here')
        booleanParam(name: 'executeTests', defaultValue: true, description ' true or false boolean')
        //you can use any of them in any stages and can be good to combine with expressions.
    }
    stages {
        stage("build") {
            steps {
                echo 'building the application ....'
            }
        }
        stage("test") {
            when {
                expression {
                    params.executeTests // using booleanparam as an example
                }
            }
            steps {
              echo 'testing the application ....'
            }
        }
         stage("deploy") {
            steps {
                echo 'deploying the application ....'
                echo "deploying  version ${params.VERSION}" //using choice parameter as an example
            }
        }
    }
}
