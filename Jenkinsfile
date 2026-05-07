pipeline {
    agent any
    environment {
        IMAGE_NAME = "notes-app:latest"
        CONTAINER_NAME = "notes-app-container"
        PORT = "9092"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/sagar9836/notes-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh '''
                echo "=======Building Docker Image========="
                docker build -t $IMAGE_NAME .
                '''
            }
        }
        // stage('Stop Old Container') {
        //     steps {
        //         sh '''
        //         echo "========Stopping Old container============"
        //         docker stop $CONTAINER_NAME || true
        //         docker rm $CONTAINER_NAME || true
        //         '''
        //     }
        // }
        // stage('Run Container') {
        //     steps {
        //         sh '''
        //         echo "=========Running New Container============="
        //         docker run -d --name $CONTAINER_NAME -p $PORT:80 -v notes-data:/data $IMAGE_NAME
        //         '''
        //     }
        // }
        // stage('Verify') {
        //     steps {
        //         sh '''
        //         echo "=========Checking app response========"
        //         sleep 5
        //         curl -s http://localhost:$PORT | head -n 20
        //         '''
        //     }
        // }
    }
    post {
        success {
            echo "Notes App Deployed Successfully"
        }
        failure {
            echo "Notes app Deployment failed. Check logs"
        }
    }
}
