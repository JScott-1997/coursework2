node {
  stage('Build') {
          //Pull Repo
          git branch: 'main', credentialsId: 'Coursework2', url: 'https://github.com/JScott-1997/coursework2'
          //Build Docker Image
          app = docker.build("jscott1997/coursework2") 
  }
  stage('test') {
    app.inside{
      sh 'echo "Passed the Test"'
    }
  }
  stage('deploy') {
    withCredentials([usernamePassword(credentialsId: "dockerhub", passwordVariable: "dockerKey", usernameVariable: "dockerUser")]){
             sh "docker login --username $dockerUser --password $dockerKey"
           }
    
    app.push("latest")
    
    sshagent(credentials : ['Build_Server']) {
      sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-52-23-230-199.compute-1.amazonaws.com 'kubectl set image deployments/coursework2 coursework2=jscott1997/coursework2'"
    }
  }
}
