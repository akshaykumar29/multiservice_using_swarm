def image
pipeline {
    environment {
        image = "22119697/ci-cd-jenkins"
        registryCredentials = "docker hub user password"
        dockerImage = ''
    }
    agent any

    stages{
        
        stage("Build Image") {

            steps {
                script {
                     image = registry + ":${env.BUILD_NUMBER}"
                     println ("${image}"
                     dockerImage = docker.build image + ":$BUILD_NUMBER"
                    
                }
            }

        

        }

        stage("Testing - running in Jenkins Node") {

            steps {
                sh "docker run -d --name ${JOB_NAME} -p 5000:5000 ${image}"
            }
        }
        stage("Push to Dockerhub") {
            steps {
                script {
                    docker.withRegistry( "https://registry.hub.docker.com", registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
     }
 }
 
 
