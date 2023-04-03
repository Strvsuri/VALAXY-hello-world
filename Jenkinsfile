pipeline {
    agent any
    tools {
        maven 'Apache Maven 3.9.1' 
        jdk 'java-11-openjdk-amd64'
    }
    environment {
        PATH="$M2_HOME/bin:$PATH"
    }
    stages {
        stage (' git checkout') {
            steps {
                git 'https://github.com/Strvsuri/VALAXY-hello-world.git'
            }
        }
        stage (' build pro') {
            steps {
                sh 'mvn clean install'
            }
        }    
    }
}
