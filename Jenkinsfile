pipeline {
    agent any
    stages {
        stage('Build-docker-image') {
            steps {
                script {
 		    loginToDockerHub()
                    buildDockerImage()
                    pushDockerImage()
                }
            }
        }
    }
}

// Login in to Docker hub
def loginToDockerHub() {
    withCredentials([usernamePassword(credentialsId: 'rolandstech-dockerhub', usernameVariable: 'DOCKERHUB_USR', passwordVariable: 'DOCKERHUB_PSW')]) {
        echo "Logging in to DockerHub..."
        sh "docker login -u $DOCKERHUB_USR -p $DOCKERHUB_PSW"
    }
}

// Build Docker image
def buildDockerImage() {
    echo "Building docker image..."
    sh "docker pull rolandstech/api-tests:latest "
    // sh "docker build -t rolandstech/api-tests:latest ."
}

// Push the image to DockerHub
def pushDockerImage() {
    echo "Pushing image to DockerHub..."
    sh "docker push rolandstech/api-tests:latest"
}
