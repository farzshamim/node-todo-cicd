pipeline {
    agent { label 'dev-agent' }
    
    stages{
        stage('code'){
            steps {
                git url: 'https://github.com/farzshamim/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('build and test'){
            steps {
                sh 'docker build . -t farzshamim/node-todo-app:latest'
            }
        }
        stage('login and push image'){
            steps {
                echo 'login into dockerhub and pushing images..'
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push farzshamim/node-todo-app:latest"
                }
            }
        }
        stage('deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
