pipeline{  
  agent any
    environment{
    IMG_NAME = 'jenkins'
    DOCKER_REPO = 'myimage_nginx'
  }
  stages {
    stage("Supprimer le workspace"){
      steps{
        deleteDir()
      }
    }    
    stage("checkout SCM"){
      steps{
        git branch: 'main', credentialsId: 'id-user', url: 'https://github.com/Yankhoba92/calculatrice.git'
      }
    } 
    stage("Buid image docker"){
      steps{
        script{
           sh "docker build -t ${IMG_NAME} ."
          sh "docker tag ${IMG_NAME} ${DOCKER_REPO}:${IMG_NAME}"
        }
    } 
  }
  stage("Deploiement application"){
      steps{
        script{
          sh "docker stop monapp || true"
          sh "docker rm monapp || true"
          sh "docker run -d --name monapp --hostname monapp -p 8599:80 ${IMG_NAME}"
          sh 'docker exec monapp "ifconfig"'
        }
    } 
  }
}
}
