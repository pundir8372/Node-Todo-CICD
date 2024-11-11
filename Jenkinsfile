pipeline {
    agent { label 'dev-server' }
    stages {
        stage("Code Clone") {
            steps {
                git url: 'https://github.com/pundir8372/Node-Todo-CICD.git', branch: 'master'
                echo "Code clone ho gya"
            }
        }
        stage("Build") {
            steps {
                sh 'docker build -t node-app .'
                echo "build ho rha ha"
            }
        }
        stage("Push Image to Dockerhub") {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: "dockerHubCreds",
                        usernameVariable: "dockerHubUser",
                        passwordVariable: "dockerHubPass"
                    )
                ]) {
                    sh 'echo ${dockerHubPass} | docker login -u ${dockerHubUser} --password-stdin'
                    sh 'docker image tag node-app:latest ${dockerHubUser}/node-app:latest'
                    sh 'docker push ${dockerHubUser}/node-app:latest'
                    echo "Image ho rhi ha dockerHub ma"
                }
            }
        }
        stage("Deploy") {
            steps {
                sh 'docker compose down && docker compose up -d --build'
                echo "Code deploy ho gya"
            }
        }
    }
}
