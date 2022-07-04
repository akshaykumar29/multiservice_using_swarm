def img
pipeline {
    environment {
        registry = "22119697/ci-cd-jenkins"
        registryCredentials = "docker hub user password"
        dockerImage = ""
    }
    agent any

    stages{
        
        stage("Build Image") {

            steps {
                script {
                     img = registry + ":${env.BUILD_ID}"
                     println ("${img}")
                     //dockerImage = docker.build("${img}")
                    sh 'docker build --tag "${img}" .' 
                    
                }
            }

        

        }

        stage("Testing - running in Jenkins Node") {

            steps {
                sh "docker run -d --name ${JOB_NAME} -p 5000:5000 ${img}"
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
 
 
