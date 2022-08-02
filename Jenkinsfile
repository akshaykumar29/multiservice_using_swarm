node{
    stage("Git CheckOut"){
        git url: 'https://github.com/akshaykumar29/py-project.git',branch: 'main'
    }
    
   
    
    stage("Build Dokcer Image") {
         sh "docker build -t akshaykumar29/swarm ."
    }
    
    stage("Docker Push"){
        withCredentials([string(credentialsId: 'docker_hub_ki', variable: 'docker_hub_ki')]) {
          sh "docker login -u akshaykumar29 -p ${docker_hub_ki}"
        }
        sh "docker push akshaykumar29/swarm"
        
    }
    
    // Remove local image in Jenkins Server
    stage("Remove Local Image"){
        sh "docker rmi -f akshaykumar29/swarm"
    }
    
    stage("Deploy to docker swarm cluster"){
        sshagent(['ssh_agent_ki']) {
		    sh 'scp -o StrictHostKeyChecking=no  docker-compose.yml ubuntu@13.233.38.224:'
		    //sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.233.38.224 docker stack rm springboot'
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.233.38.224 docker stack deploy --prune --compose-file docker-compose.yml teststack'
        }
    }
}
