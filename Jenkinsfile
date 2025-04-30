pilpileine{
  agent any
  stages{
    stage("Supprimer le workspace"){
      steps{
        deleteDir()
      }
    }    
    stage("checkout SCM"){
      steps{
        sh 'git clone https://github.com/Yankhoba92/calculatrice.git'
      }
    } 
  }
}
