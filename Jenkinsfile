pipeline{  
  agent any
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
          sh 'docker build -t myimage_nginx .'
          sh 'docker tag myimage_nginx med:myimage_nginx'
        }
    } 
  }
  stage("Deploiement application"){
      steps{
        script{
          sh 'docker image rm myimage_nginx'
          sh 'docker stop monapp'
          sh 'docker rm monapp'
          sh 'docker rm -f $(docker ps -a)'
          sh 'docker run -d --name monapp --hostname monapp -p 8099:80 myimage_nginx'
          sh 'docker exec -ti monapp "ifconfig"'
        }
    } 
  }
}
}
