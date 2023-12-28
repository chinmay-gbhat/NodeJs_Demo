pipeline {
    agent { Label "Node_02" } 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('NodeJSApp')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/chinmay-gbhat/NodeJs_Demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t chinmaygbhat/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push chinmaygbhat/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

