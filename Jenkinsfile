pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "omarmansor/train-schedule"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh 'gradle build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
       
    }
}
