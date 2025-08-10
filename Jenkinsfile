pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials("31adf442-5009-4900-b4b4-a7f2f66de395")
  }
  stages {
    stage('Clone Repository') {
      agent {
        label "KM"
      }
      steps {
        script {
          git 'https://github.com/dakshdotintellipaat/website.git' 
        }
      }
    }
    stage('Docker Build & Push') {
      agent {
        label "KM" 
      }
      steps {
        script {
          sh 'sudo docker build . -t souravhajra12345/devops2' 
          sh 'sudo docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}' 
          sh 'sudo docker push souravhajra12345/devops2' 
        }
      }
    }
    stage('Kubernetes Deployment') {
      agent {
        label "KM"
      }
      steps {
        script {
          sh 'kubectl apply -f kube.yml'
        }
      }
    }
  }
}