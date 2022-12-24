pipeline {
    agent any
        tools {
        jdk "myjava"
    }

    environment {
        DOCKER_IMAGE_NAME = "omarmansor/train-schedule"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
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
            environment { 
                DOCKER_HUB_LOGIN = 'docker_hub_login'
            }
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
