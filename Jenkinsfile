@Library('shared-lib')_
pipeline {
    agent any
    environment {
                Dockerhub = 'DockerHub'
	    	imageName = ' ahmedmoo/nti'
            }
    
     stages {
     
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
		

//        stage('Push Docker Image to Docker Hub') {
//         
//            steps {
//                script {
//                    echo " pushing the image "
//                    withCredentials([usernamePassword(credentialsId: "${Dockerhub}", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
//				          sh "docker login -u ${USERNAME} -p ${PASSWORD}"
//        		    }
//                    sh " docker push ${imageName} "
//                   }
//                }
//	}

	stage ('Push the image to my docker hub') {
		steps{
			PushDockerimage("${Dockerhub}","${imageName}")
		}
	}

//	stage ('EditImageName') {
//		steps {
//			script {
//				dir ('.') {
//					EditImageName("${imagName}")
//				}
//			}
//		
//			
//		}
//	}


	stage ('Editin the image name') {
		steps {
			script {

				   dir('k8s') {	
					  sh "sed -i 's|image:.*|image: ${imageName}|g' deploym.yaml"
			
				   }
			}
		}
	}
  }
 }


