pipeline {
    agent any

    stages {
        stage('Code') {
            steps {
                echo 'Cloning Code...'
                git url: "https://github.com/SAJanGAIKwad/SAJAN.git", branch: 'main'
                echo 'Code Pulled Successfully'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the project...'
                bat "docker build -t portfolio:latest ."
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Push to DockerHub') {
            steps {
                echo 'Pushing Image to DockerHub'
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCred",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser")]) {
                    bat "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    bat "docker image tag portfolio:latest ${env.dockerHubUser}/portfolio:latest"
                    bat "docker push ${env.dockerHubUser}/portfolio:latest"
                }
            }
        }

        stage('Deploy') {
        steps {
            echo 'Deploying the Docker container...'
            bat "docker run -d -p 80:80 portfolio:latest"
            }
        }
    }
}

