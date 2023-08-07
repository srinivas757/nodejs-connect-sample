pipeline {
  agent any
  stages{
    stage("build"){
      steps{
        sh "sudo docker build -t srinivas757:$Build number ."
      }
    }

    stage("Deploy"){
      steps{
        sh "sudo docker run itd -p 3000:3000 --name srinivas srinivas757:$Build number"
      
      }
    }
  }

}
