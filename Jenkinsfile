pipeline {
    agent any
    environment {
        registryCredential = 'dockerhubcred'   // Credential ID in Jenkins
        imageName = 'jenkins_my-docker-image'   // Image name (be sure this matches your Docker Hub repo)
        imageTag = 'latest'                    // Image tag
        dockerHubRepo = 'pawbabe'    // Your Docker Hub username
  }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Pawbabe/Tire-shop.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package' // Use 'mvn clean install' if using Maven
            }
        }   
        stage('Converting Docker Image') {
           steps {
              echo 'Building Docker Image'
              script {
          // Build the Docker image and capture it into the dockerImage variable
                  dockerImage = docker.build("${dockerHubRepo}/${imageName}:${imageTag}", ".")
        }
      }
    }
        stage('Pushing Image') {
          steps {
            echo 'Pushing Docker Image to Docker Hub'
            script {
              // Authenticate to Docker Hub and push the built image
              docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                // Push the image
                dockerImage.push("${imageTag}")
          }
        }
      }
  
    }

}
