@Library('https://github.com/ahmedmostafa56389/shared_library.git')_
pipeline {
    agent any
    environment {
                Dockerhub = 'DockerHub'
	    	imageName = ' ahmedmoo/nti:latest '
            }
    
 //   stages {
     
   //     stage('Build Docker Image') {
     //       steps {
       //         script {
         //           sh ' docker build -t ${imageName}  . '
           //     }
          //  }
//}


	stage('Build using shared-library') {
		steps {
			BuildDockerImage("${imageName}")
		}
	}
		

        stage('Push Docker Image to Docker Hub') {
         
            steps {
                script {
                    echo " pushing the image "
                    withCredentials([usernamePassword(credentialsId: "${Dockerhub}", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
				          sh "docker login -u ${USERNAME} -p ${PASSWORD}"
        		    }
                    sh " docker push ${imageName} "
                   }
                }
            
  }
 }


