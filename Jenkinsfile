pipeline{
    agent any
    stages{
        stage("fetch"){
            steps{
            git url:"https://github.com/addit10/django-notes-app.git", branch: "main"
        }}
        stage("build"){
            steps{
                sh "docker build -t myapp ."}
        }
        stage("push"){
            steps{
                echo "pushing code to repo"
                withCredentials([usernamePassword(credentialsId:"dockerhub", passwordVariable:"dockerpass", usernameVariable:"dockeruser")]){
                 sh "docker login -u ${env.dockeruser} -p ${env.dockerpass}"
                 sh "docker tag myapp:latest ${env.dockeruser}/myapp:latest"
                 sh "docker push ${env.dockeruser}/myapp:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                echo "deploying app"
                sh "docker-compose down && docker-compose up -d"
                
            }
            
        }
    }
}
