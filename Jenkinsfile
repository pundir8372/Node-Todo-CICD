@Library('Shared')_ 
pipeline {
    agent { label 'dev-server' }
    stages {
        stage("Code Clone") {
            steps {
              
                clone('https://github.com/pundir8372/Node-Todo-CICD.git', 'master')
            }
        }
        stage("Build") {
            steps {
                
                dockerbuild('node-app', 'latest')
            }
        }
        stage("Push to DockerHub"){
            steps{
                dockerpush("dockerHubCreds", "node-app" , "latest")
            }
        }
        
        stage("Deploy") {
            steps {
               
                echo 'Deploying the application...'
                deploy()
            }
        }
        
    }
}
