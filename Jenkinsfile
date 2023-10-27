pipeline {
  agent any
  environment {
     registryUrl ="https://7tiuxysa.c1.gra9.container-registry.ovh.net"
  }
  stages{
	  stage('building Docker Image') {
	    steps {
		    script {
            sh 'docker build -t materialdashboard:latest .'
        }
	    }
	  }

    stage('Upload Image to Harbor registry') {
      steps{   
        script {
          // sh '''echo $DOCKER_CREDENTIALS_PSW | docker login $registryUrl -u 'DOCKER_CREDENTIALS_USER' --password-stdin'''
          sh "echo \${DOCKER_CREDENTIALS_PSW} | docker login ${registryUrl} -u \${DOCKER_CREDENTIALS_USER} --password-stdin"
          sh "docker tag materialdashboard:latest ${registryUrl}/mydemoproject/harborimg:${env.BUILD_NUMBER}"
          sh "docker image push ${registryUrl}/mydemoproject/harborimg:${env.BUILD_NUMBER}"
          sh "docker rmi materialdashboard:latest"
        }
      }
    }
  }  
}