pipeline {
  agent any
  stages{
    stage("build"){
      steps{
        sh "sudo docker build -t srinivas757:$BUILD_NUMBER ."
      }
    }

    stage("Test"){
      steps{
        sh 'trivy image --scanners vuln --format template --template /usr/local/share/trivy/templates/html.tpl -o report.html srinivas757:$BUILD_NUMBER'
        sh "cp report.html $WORKSPACE"
      
      }
    }
    
    stage("Deploy"){
      steps{
        sh "sudo docker stop srinivas"
        sh "sudo docker rm srinivas"
        sh "sudo docker run -itd -p 3000:3000 --name srinivas srinivas757:$BUILD_NUMBER"
      
      }
    }

    stage("Push"){
      steps{
        sh "sudo cat my-password | sudo docker login -u srinivas757 --password-stdin"
        sh "sudo docker tag srinivas757:$BUILD_NUMBER srinivas757/srinivas:$BUILD_NUMBER"
        sh "sudo docker push srinivas757/srinivas:$BUILD_NUMBER"
      
      }
    }
  }
    post {
        always {
            archiveArtifacts artifacts: 'treport.html', allowEmptyArchive: true
        }
    }

}
