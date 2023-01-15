pipeline {
  agent any
    
  stages {
     
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t udagram-api-feed ./udagram-api-feed'
        sh 'docker build -t udagram-api-user ./udagram-api-user'
        sh 'docker build -t udagram-frontend ./udagram-frontend'
        sh 'docker build -t udagram-reverseproxy ./udagram-reverseproxy'
      }
    }
    stage('Docker Push') {
    	agent any
      steps {
      	withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push liavklt/udagram-api-feed:v1'
          sh 'docker push liavklt/udagram-api-user:v1'
          sh 'docker push liavklt/udagram-frontend:v1'
          sh 'docker push liavklt/udagram-reverseproxy:v1'
        }
      }  
    
  }
}
}