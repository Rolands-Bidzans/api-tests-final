pipeline {
    agent any
        parameters {
    	string(name: 'dockerhub_username', defaultValue: 'rolandstech', description: 'Dockerhub username')
    }
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
        bat "docker login -u $DOCKERHUB_USR -p $DOCKERHUB_PSW"
    }
}

// Build Docker image
def buildDockerImage() {
    echo "Building docker image..."
    bat "docker build -t ${params.dockerhub_username}/api-tests:latest ."
}

// Push the image to DockerHub
def pushDockerImage() {
    echo "Pushing image to DockerHub..."
    bat "docker push ${params.dockerhub_username}/api-tests:latest"
}
