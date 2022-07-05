def image
pipeline {
    environment {
        registry = "22119697/pipline"
        registryCredential = 'docker_hub'
        dockerImage = ''
    }
    agent any

    stages{
        
        stage("Build Image") {

            steps {
                script {
                     image = registry + ":${env.BUILD_NUMBER}"
                     println ("${image}")
                     dockerImage = docker.build image
                    
                }
            }

        

        }

        stage("Testing - running in Jenkins Node") {

            steps {
                sh "docker run -d --name ${JOB_NAME} -p 5000:5000 ${image}"
            }
        }
        stage('Cleaning up') {
             steps {
                 sh "docker rm -f ${JOB_NAME}"
               }
        }
        stage("Push to Dockerhub") {
            steps {
                script {
                    docker.withRegistry('', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage("running in staging") {
            
            def remote = [:]
            remote.name = “ubuntu
            remote.host = "3.144.212.131"
            remote.allowAnyHosts = true
            stage('Remote SSH') 
            {
            sshCommand remote: remote, command: "ls -lrt"
            sshCommand remote: remote, command: "for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done"
    
            }

            }
           }
       }   
 }
 
}
