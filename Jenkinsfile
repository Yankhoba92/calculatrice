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
          sh 'docker run -d --name monapp01 --hostname monapp01 -p 8099:80 myimage_nginx'
          sh 'docker exec  monapp01 "ifconfig"'
        }
    } 
  }
}
}
