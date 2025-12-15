pipeline {
    agent any
    tools {
        jdk 'jdk17'
        nodejs 'node16'
    }
    stages {
        stage ("Clean Workspace") {
            steps {
                cleanWs()
            }
        }
        stage ("Git Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/Tirupatitata123/Startbucksclone-aaplication.git'
            }
        }
        stage("Install NPM Dependencies") {
            steps {
                sh "npm install"
            }
        }
        stage("Build Docker Image") {
            steps {
                sh "docker build -t starbucks ."
            }
        }
        stage("Tag & Push to DockerHub") {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker') {
                        sh "docker tag starbucks tirupatipallu/cicd:1.0.0"
                    //imagetag <username>/<docker repository>
                        sh "docker push tirupatipallu/starbucks:1.0.0"
                        //<username>/<image-name>
                    }
                }
            }
        }
    }
}
