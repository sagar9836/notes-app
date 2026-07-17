pipeline {

    agent any

    environment {
        IMAGE_NAME = "notes-app:latest"
        CONTAINER_NAME = "notes-app-container"
        PORT = "9092"
        DOCKER_HUB_USER = "9836sagar9836"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/sagar9836/notes-app.git'
            }
        }

        stage('Build Docker Image') {

            steps {

                sh '''
                echo "======= Building Docker Image ========="

                echo "Running as user: $(whoami)"

                echo "======= Running Containers ========="
            

                echo "======= Docker Images ========="
              
                '''
            }
        }

        stage('Docker Login & Push') {

            steps {

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub_creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {

                    sh '''
                    echo "======= Logging in to DockerHub ========="

                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }
    }

    post {

        success {

            echo "Notes App Deployed Successfully 🚀"

            emailext(
                subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",

                body: """
                <h2>Build Successful 🚀</h2>

                <p><b>Job Name:</b> ${env.JOB_NAME}</p>

                <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>

                <p><b>Status:</b> SUCCESS</p>

                <p><b>Build URL:</b> ${env.BUILD_URL}</p>
                """,

                to: "sagarpaal9836@gmail.com",

                mimeType: "text/html"
            )
        }

        failure {

            echo "Notes App Deployment Failed ❌"

            emailext(
                subject: "❌ FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",

                body: """
                <h2>Build Failed 💀</h2>

                <p><b>Job Name:</b> ${env.JOB_NAME}</p>

                <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>

                <p><b>Status:</b> FAILURE</p>

                <p><b>Check Console Output:</b> ${env.BUILD_URL}</p>
                """,

                to: "sagarpaal9836@gmail.com",

                from: "sagarpaal116@gmail.com",

                replyTo: "sagarpaal116@gmail.com",

                mimeType: "text/html",

                attachmentsPattern: "trivyfs.txt"
            )
        }
    }
}    






    
// pipeline {
//     agent {
//         label 'agent-1'
//     }
//     environment {
//         IMAGE_NAME = "notes-app:latest"
//         CONTAINER_NAME = "notes-app-container"
//         PORT = "9092"
//     }
//     stages {
//         stage('Checkout') {
//             steps {
//                 git branch: 'master', url: 'https://github.com/sagar9836/notes-app.git'
//             }
//         }
//         stage('Build Docker Image') {
//             steps {
//                 sh '''
//                 echo "=======Building Docker Image========="
                
//                 echo "$whoami"
//                 echo " build ho rha h"
//                 '''
//             }
//         }
//         // stage('Stop Old Container') {
//         //     steps {
//         //         sh '''
//         //         echo "========Stopping Old container============"
//         //         docker stop $CONTAINER_NAME || true
//         //         docker rm $CONTAINER_NAME || true
//         //         '''
//         //     }
//         // }
//         // stage('Run Container') {
//         //     steps {
//         //         sh '''
//         //         echo "=========Running New Container============="
//         //         docker run -d --name $CONTAINER_NAME -p $PORT:80 -v notes-data:/data $IMAGE_NAME
//         //         '''
//         //     }
//         // }
//         // stage('Verify') {
//         //     steps {
//         //         sh '''
//         //         echo "=========Checking app response========"
//         //         sleep 5
//         //         curl -s http://localhost:$PORT | head -n 20
//         //         '''
//         //     }
//         // }
//     }
//     post {
//         success {
//             echo "Notes App Deployed Successfully"
//         }
//         failure {
//             echo "Notes app Deployment failed. Check logs"
//         }
//     }
// }
