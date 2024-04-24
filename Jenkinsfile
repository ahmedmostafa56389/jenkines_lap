@Library('shared-lib')_
pipeline {
    agent any
    environment {
                Dockerhub = 'DockerHub'
	    	imageName = ' ahmedmoo/nti'
	    	k8s = ' KubeCred '
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
//				dir ('k8s') {
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

//	stage (' deploy ' ) {
//		steps {
//			script {
//				  withCredentials([file(credentialsId: "${k8s}", variable: 'KUBECONFIG_FILE')]) {
//					      sh "export KUBECONFIG=${KUBECONFIG_FILE} && kubectl apply -f ./k8s"
//			          }
//			}
//		}
//	}
				
  
  	stage ( ' deploy ' ) {
	     steps { 
		     script {
			     dir ('k8s') {
			     		Deployonk8s ("${k8s}")
		     	     }
		     }
	     }
	}
     
     }
      post {
        success {
            echo "${JOB_NAME}-${BUILD_NUMBER} pipeline succeeded"
        }
        failure {
            echo "${JOB_NAME}-${BUILD_NUMBER} pipeline failed"
        }
    }
 }


