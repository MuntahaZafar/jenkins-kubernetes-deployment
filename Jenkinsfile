pipeline {

  environment {
    dockerimagename = "bravinwasike/react-app"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/MuntahaZafar/jenkins-kubernetes-deployment.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build jenkins-kubernetes-deployment
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'https://hub.docker.com/repository/docker/muntahazafar/jenkins-kubernetes-deployment'
           }
      steps{
        script {
          docker.withRegistry( 'https://hub.docker.com/repository/docker/muntahazafar/jenkins-kubernetes-deployment', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }

  }

}
