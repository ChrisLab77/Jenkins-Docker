pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('Jenkins_dockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'docker build -t chrislab77/myapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push chrislab77/myapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
