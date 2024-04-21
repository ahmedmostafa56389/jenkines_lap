pipeline {
    agent any
    environment {
                Dockerhub = 'DockerHub'
            }
    
    stages {
     
        stage('Build Docker Image') {
            steps {
                script {
                    sh ' docker build -t ahmedmoo/nti:latest  . '
                }
            }
}

        stage('Push Docker Image to Docker Hub') {
         
            steps {
                script {
                    echo " pushing the image "
                    withCredentials([usernamePassword(credentialsId: "${dockerHubCredentialsID}", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
				          sh "docker login -u ${USERNAME} -p ${PASSWORD}"
        		    }
                    sh " docker push ahmedmoo/nti:latest "
                   }
                }
            
  }
 }
}

