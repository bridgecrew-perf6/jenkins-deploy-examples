def git_address = "https://github.com/chenhxbj/jenkins-deploy-examples.git"
def k8s_auth = "2280f8d7-6668-4d3a-9f78-705dcaa8cf63"

podTemplate(label: 'jenkins-slave', cloud: 'kubernetes', containers: [
    containerTemplate(
        name: 'jnlp', 
        image: "jenkins/jnlp-slave:latest"
    ),
    containerTemplate(
        name: 'docker', 
        image: "docker:stable",
        ttyEnabled: true,
        command: 'cat'
    ),
  ],
  volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
  ],
) 
{
  node("jenkins-slave"){
      stage('拉取代码'){
          checkout([$class: 'GitSCM', branches: [[name: 'master']], userRemoteConfigs: [[url: "${git_address}"]]])
      }
      stage('部署项目'){
          kubernetesDeploy configs: "nginx.yml", kubeconfigId: "${k8s_auth}"
      }
  }
}
