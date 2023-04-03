pipeline {
    agent any
    tools {
        maven 'maven' 
        jdk 'java'
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
