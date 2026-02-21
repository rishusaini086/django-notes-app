@Library("shared") _

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
                script{
                    clone("https://github.com/rishusaini086/django-notes-app.git","main")
                }
            }
        }
        stage('Build Code'){
            steps{
                script{
                    docker_build("rajatkumar416","django-notes-app","latest")
                }
            }
        }
        stage("Push to DockerHub"){
            steps{
                script
                    {
                        docker_push("rajatkumar416","django-notes-app","latest")
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
                script{
                    docker_deploy()
                }
            }
        }
    }
}