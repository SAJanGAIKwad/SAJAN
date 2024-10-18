@Library("Shared") _
pipeline {
    agent any

    stages {
        stage('Hello')
        {
            steps{
                script{
                    hello()
                }
            }
        }
        
        stage('Code') {
            steps {
                script{
                    clone("https://github.com/SAJanGAIKwad/SAJAN.git", "main")
                }
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building the project...'
                script{
                    docker_build("portfolio", "latest", "sajangaikwad2002")
                }
                
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        
        stage('Push to DockerHub') {
            steps {
                script{
                    docker_push("portfolio", "latest", "sajangaikwad2002")
                }
            }
        }

        stage('Deploy') {
            steps {
                script{
                    docker_compose()
                }
        
            }
        }
    }
}
