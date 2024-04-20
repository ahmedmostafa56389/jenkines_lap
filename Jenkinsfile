pipeline{
  agent any
  
  environment{
    Dockercred  = 'DockerHub'
  }

  stages{
    
    stage ('Test'){
       steps{
         script{
           echo " test running"
           sh 'pytest' // Run Python tests
       }
      }
    }

    
    stage('BUILD'){
      steps {
        script {
          sh ' docker build -t ahmedmoo/nti:latest'
          echo " image built "
        }
      }
    }

    
    stage('push'){
      steps{
        script {
        		echo "pushing docker image ..."
		      	withCredentials([usernamePassword(credentialsId: "${Dockercred}", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
		        		sh "docker login -u ${USERNAME} -p ${PASSWORD}"
        		}
             sh "docker push ahmedmoo/nti:latest"
      }
    }
   }
}

post { 
  success {
    echo " ahmed mostafa"
  }
  failure {
    echo " fail yaa ibny"
  }
}
}

          
      
    
