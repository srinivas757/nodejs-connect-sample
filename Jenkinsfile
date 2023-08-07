pipeline {
  agent any
  stages{
    stage("build"){
      steps{
        sh "sudo docker build -t srinivas757:$BUILD_NUMBER ."
      }
    }

    stage("Deploy"){
      steps{
        sh "sudo docker stop srinivas"
        sh "sudo docker rm srinivas"
        sh "sudo docker run -itd -p 3000:3000 --name srinivas srinivas757:$BUILD_NUMBER"
      
      }
    }
  }

}
