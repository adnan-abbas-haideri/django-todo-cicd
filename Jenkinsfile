pipeline {
    agent {label '007'}
    stages{
        stage('code'){
            steps{
                echo "This is cloning the code"
                git url: "https://github.com/adnan-abbas-haideri/django-todo-cicd", branch: "main"
                echo "Code Clone Sucessfull"
            }
        }
        stage('build'){
            steps{
                sh "whoami"
                echo "This is building the code"
                sh "docker build -t todo-app:latest ."
            }
        }
        stage('Push to DockerHub'){
            steps{
                echo "This is pushing the image to GockerHub"
                withCredentials([usernamePassword(
                    credentialsId:"aa17f279-a000-421e-8e22-ac321947ae95",
                    usernameVariable:"dockerHubUser", 
                    passwordVariable:"dockerHubPass")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag todo-app:latest ${env.dockerHubUser}/notes-todo:latest"
                sh "docker push ${env.dockerHubUser}/notes-todo:latest"
                    }
            }
        }
        stage('deploy'){
            steps{
                
                echo "This is deploying the code"
                sh "docker compose up -d "
            }
        }
        
    }
}
