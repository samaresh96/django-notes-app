pipeline{
    agent any
    
    stages {
        stage("code clone"){
            steps{
                echo "cloning the code"
                git url:"https://github.com/samaresh96/django-notes-app", branch: "main"
            }
            
            
        }
        stage("build"){
            steps {
                 echo "building the code"
                 sh "docker build -t my-notes-app ."
                
            }
           
            
        }
        stage("push to dockerhub"){
            steps {
                echo "pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerpass",usernameVariable:"dockerhubuser")]){
                    sh "docker tag my-notes-app ${env.dockerhubuser}/my-notes-app:latest"
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerpass}"
                    sh "docker push ${env.dockerhubuser}/my-notes-app:latest"
                }
            }
                
            
            
            
            
        }
        stage("deploy"){
            steps {
                 echo "deploying the container"
                 sh "docker run -d -p 8000:8000 samaresh96/my-notes-app"
            }
           
        }
    }
    
}
