pipeline {
    agent any
    tools{
        maven 'maven-3.9'
    }
    stages {
        stage('increment version'){
            steps{
                script {
                echo 'incrementing app version ...'
                sh 'mvn build-helper:parse-version versions:set \
                    -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} \
                    versions:commit '
                def matcher = readFile('pom.xml')  =~ '<version>(.+)</version>'
                def version = matcher[0][1]
                env.IMAGE_NAME = "$version-$BUILD_NUMBER"

                }
            }
        }
        stage("build app") {
            steps {
                script {
                    echo "building the application ..."
                    sh 'mvn clean package'
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building the docker image ..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]){
                        sh "docker build -t ilo2003/testing:${IMAGE_NAME} ."
                        sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                        sh "docker push ilo2003/testing:${IMAGE_NAME}"
                    }
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
                            withCredentials([string(credentialsId: 'github-token', variable: 'TOKEN')]){
                                sh 'git config --global user.email "jenkins@example.com"'
                                sh 'git config --global user.name "jenkins"'

                                sh 'git status'
                                sh 'git branch'
                                sh 'git config --list'
                                sh "git remote set-url origin https://${TOKEN}@github.com/ILO2003/Module8.git"
                                sh 'git add .'
                                sh 'git commit -m "CI: version bump"'
                                sh 'git push origin HEAD:jenkins-jobs'
                            }
                        }
                    }
                }
    }
}