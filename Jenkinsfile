pipeline {
    agent { label 'vinod' }
    stages{
        stage('WorkSpace Cleanup'){
            steps{
                cleanWs()
            }
        }
        stage('Clone Code'){
            steps{

                   git url:"https://github.com/rishusaini086/django-notes-app.git", branch:"main"
            }
        }
        stage('Build Code'){
            steps{
                echo "Building the code"
                sh "docker build -t django-notes-app:latest ."
                echo "Build Completed"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword('credentialsId':"docker-creds",passwordVariable:"dockerPass",usernameVariable:"dockerUser")]){
                    sh "docker login -u ${dockerUser} -p ${dockerPass}"
                    sh "docker image tag django-notes-app:latest ${dockerUser}/django-notes-app:latest "
                    sh "docker push ${dockerUser}/django-notes-app:latest"
                }
                
            }
        }
        stage('Test Code'){
            steps{
                echo "Testing the code"
            }
        }
        stage('Deploying Code'){
            steps{
                echo "Deploying the code"
                sh "docker compose up -d"
            }
        }
    }
}