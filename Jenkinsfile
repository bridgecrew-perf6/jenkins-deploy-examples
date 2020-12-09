pipeline {
  agent any

  stages {
    stage('Pull Source Code') {
      steps {
        git branch: 'master', url: 'https://github.com/chenhxbj/jenkins-deploy-examples.git'
      }
    }

    stage('Deploy to kubernetes') {
      steps {
        kubernetesDeploy(enableConfigSubstitution: false, kubeconfigId: '2280f8d7-6668-4d3a-9f78-705dcaa8cf63', configs: '*.yml')
      }
    }
  }
}
