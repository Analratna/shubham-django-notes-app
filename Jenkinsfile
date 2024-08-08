pipeline{
    agent any
    stages{
        stage("Clone code"){
            steps{
                echo "Cloning the code"
                git url:"https://github.com/Analratna/shubham-django-notes-app.git", branch: "main"
            }
        }
        stage("build"){
            steps{
                echo "building the image"
                
                sh "docker build -t my-note-app ."
            }
        }
        stage("push to DockerHub"){
            steps{
                echo "pushing the code to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerHub", passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p  ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                    
                }
            }
        }
    
        stage("deploy"){
            steps{
                echo "deploying the container"
                sh "docker-compose down && docker-compose up -d"

            }
        }
    }
}
