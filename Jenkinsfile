pipeline {
    agent any
    
    stages {
        stage('Test Python Code') {
            steps {
                sh 'pytest' // تشغيل اختبارات البايثون
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('ahmedmoo/nti:latest') 
                }
            }
}

        stage('Push Docker Image to Docker Hub') {
            environment {
                DOCKERHUB_CREDENTIALS = credentials('DockerHub')
            }
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'DockerHub') {
                        docker.image('ahmedmoo/nti:latest').push() 
                    }
                }
            
}
}
}
}
