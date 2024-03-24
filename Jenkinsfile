pipeline {
    agent any
    stages {
        stage("test") {
            steps {
                script{
                    echo 'Testing the application ....'
                    echo "Executing pipeline for branch $BRANCH_NAME"
                }
            }
        }
        stage("build") {
            steps {
                script{
                    echo 'Building the application ....'
                }
            }
        }
         stage("deploy") {
            steps {
                script{
                    echo 'Deploying the application ....'
                }
            }
        }
        stage("commit version update") {
                    steps {
                        script {
                            withCredentials([usernamePassword(credentialsId: 'github-credentials', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]){
                                sh 'git config --global user.email "jenkins@example.com"'
                                sh 'git config --global user.name "jenkins"'

                                sh 'git status'
                                sh 'git branch'
                                sh 'git config --list'
                                sh "git remote set-url origin https://${USERNAME}:${PASSWORD}@github.com/ILO2003/Module8.git"
                                sh 'git add .'
                                sh 'git commit -m "CI: version bump"'
                                sh 'git push origin HEAD:jenkins-jobs'
                            }
                        }
                    }
                }
    }
}
