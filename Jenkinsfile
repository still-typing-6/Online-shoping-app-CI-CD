pipeline{
    agent any
    stages{
        stage("fetch"){
            steps{
                git url: "https://github.com/still-typing-6/Online-shoping-app-CI-CD.git", branch: "master"
            }
        }
        stage("build"){
            steps{
                sh "docker build -t online-shopping-app:latest ."
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: 'dockerHubCreds',
                    usernameVariable: 'API_USER',
                    passwordVariable: 'API_Pass'
                    )]){
                        sh "docker login -u ${env.API_USER} -p ${env.API_Pass}"
                        sh "docker image tag online-shopping-app:latest ${env.API_USER}/online-shopping-app:latest"
                        sh "docker push ${env.API_USER}/online-shopping-app:latest"
                }
            }
        }
        stage("run"){
            steps{
                sh "docker compose up -d"
            }
        }
    }
}
