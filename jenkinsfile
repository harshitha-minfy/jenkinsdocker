pipeline {
    agent any

    environment {
        IMAGE_NAME = 'harshitha/python-demo'
        CONTAINER_NAME = 'python-demo-container'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any running container with same name
                    sh """
                        docker rm -f $CONTAINER_NAME || true
                        docker run --name $CONTAINER_NAME $IMAGE_NAME
                    """
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
            sh 'docker ps -a'
        }
    }
}
