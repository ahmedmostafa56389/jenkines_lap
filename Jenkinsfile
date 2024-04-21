pipeline {
    agent any
    environment {
                DOCKERHUB_CREDENTIALS = credentials('DockerHub')
            }
    
    stages {
     
        stage('Build Docker Image') {
            steps {
                script {
                    sh ' docker build -t ahmedmoo/nti:latest  . '
                }
            }
}

     //   stage('Push Docker Image to Docker Hub') {
         
         //   steps {
           //     script {
             //       docker.withRegistry('https://index.docker.io/v1/', 'DockerHub') {
               //         docker.image('ahmedmoo/nti:latest').push() 
                 //   }
                //}
            
//}
//}
}
}
