@Library("Shared") _
pipeline {
    agent { label "faizan" }

    stages {
        
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Code") {
            steps {
                script{
                clone("https://github.com/Muhammad-Faizan-Qureshi/django-notes-app.git","main")
                }
            }
        }

        stage("Build") {
            steps {
                script{
                docker_build("django-notes-app", "latest", "white10001")
                }
            }
        }

        
        stage("Push to Dockerhub") {
            steps {
                echo "Pushing images using Shared Library"
                script {
                docker_push("dockerHubCred", "django_app", "django-notes-app")
                docker_push("dockerHubCred", "nginx", "django-notes-nginx")
                     }
           }
       }

        stage("Deploy") {
            steps {
                echo "Deploying the application"
                sh "docker compose up -d --remove-orphans"
                sh "docker compose ps"
            }
        }
    }
}
