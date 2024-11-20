pipeline {
    agent any

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
  
    }

}
