pipeline {

  environment {
    dockerimagename = "muntahazafar/jenkins-kubernetes-deployment"
    dockerImage = ""
  }

  agent any

  stages {

/*    stage('Checkout Source') {
      steps {
        git checkout 'https://github.com/MuntahaZafar/jenkins-kubernetes-deployment.git'
      }
    }  */

    stage('Build image') {
      steps{
        script {
          sh "docker -v"
          sh "docker build -f $WORKSPACE/Dockerfile -t muntahazafar/jenkins-kubernetes-deployment." 
          sh 'docker tag muntahazafar/jenkins-kubernetes-deployment'
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
