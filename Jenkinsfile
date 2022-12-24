pipeline {
    agent any
        tools {
        jdk "myjava"
    }

    environment {
        DOCKER_IMAGE_NAME = "omarmansor/train-schedule"
        DOCKER_HUB_LOGIN = 'docker_hub_login'
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                    app.inside {
                        sh 'echo Hello, World!'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_LOGIN) {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
