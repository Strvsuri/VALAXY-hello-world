pipeline {
    agent any
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
        stage ('copying artifacts') {
            steps {
                sshagent(['687a60ca-45ca-4284-945e-3a0fd25af5ee']) {
                    sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ubuntu@172.31.83.97:/opt'
                }
            }
        }
    }
}
