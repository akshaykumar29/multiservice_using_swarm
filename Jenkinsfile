node{
    stage("Git CheckOut"){
        git url: 'https://github.com/akshaykumar29/py-project.git',branch: 'main'
    }
    
   
    
    stage("Build Dokcer Image") {
         sh "docker build -t akshaykumar29/swarm --target img1 ."
         sh "docker build -t akshaykumar29/swarm2 --target img2 ."
    }
    
    stage("Docker Push"){
        withCredentials([string(credentialsId: 'docker_hub_ki', variable: 'docker_hub_ki')]) {
          sh "docker login -u akshaykumar29 -p ${docker_hub_ki}"
        }
        sh "docker push akshaykumar29/swarm"
        sh "docker push akshaykumar29/swarm2"
        
    }
    
    // Remove local image in Jenkins Server
    stage("Remove Local Image"){
        sh "docker rmi -f akshaykumar29/swarm"
        sh "docker rmi -f akshaykuamr29/swarm2"
    }
    
    stage("Deploy to docker swarm cluster"){
        sshagent(['ssh_agent_ki']) {
		    sh 'scp -o StrictHostKeyChecking=no  docker-compose.yml ubuntu@3.110.186.135:'
		    //sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.110.186.135 docker stack rm demostack'
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@3.110.186.135 docker stack deploy --prune --compose-file docker-compose.yml demostack'
        }
    }
}
