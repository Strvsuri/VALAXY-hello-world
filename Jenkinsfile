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
        stage ('copying artifact') {
            steps {
                sshagent(['2dbce869-b5bd-49ea-acb5-2591a8930933']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.15.55'
                    sh 'scp webapp/target/webapp.war ubuntu@172.31.15.55:/opt'
                    sh 'scp ./Dockerfile ubuntu@172.31.15.55:/opt'
                }
            }
        }    
        stage ('Building docker image') {
           steps {
                sshagent(['2dbce869-b5bd-49ea-acb5-2591a8930933']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.15.55'
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.15.55 docker image build -t $JOB_NAME:v1.$BUILD_ID /opt'
                }
            }
        }
        stage ('docker image tagging') {
            steps {
                sshagent(['2dbce869-b5bd-49ea-acb5-2591a8930933']) {
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.15.55 cd /opt'
                    sh 'scp ./*.yml ubuntu@172.31.15.55:/opt'
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.15.55 docker tag $JOB_NAME:v1.$BUILD_ID suribau/$JOB_NAME:v1.$BUILD_ID'
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.15.55 docker tag $JOB_NAME:v1.$BUILD_ID suribau/$JOB_NAME:v1.latest'
                }
            }
        }
        stage ('docker image push') {
            steps {
                sshagent(['2dbce869-b5bd-49ea-acb5-2591a8930933']) {
                    withCredentials([usernameColonPassword(credentialsId: 'd78cb8d8-8344-4c23-9158-d9ac1e030ce0', variable: 'passwd')]) {
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.15.55 docker image push suribau/$JOB_NAME:v1.$BUILD_ID'
                        sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.15.55 docker image push suribau/$JOB_NAME:v1.latest'
                    }
                }
            }
        }
    }
}

