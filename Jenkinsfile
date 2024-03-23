pipeline {
    agent any
    tools{
        maven: "maven-3.9"
    }
    stages {
        stage("build") {
            steps {
                echo 'building the application ....'
            }
        }
        stage("test") {
            steps {
              echo 'testing the application ....'
            }
        }
         stage("deploy") {
            steps {
                echo 'deplyoing the application ....'
            }
        }
    }
}
