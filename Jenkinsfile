pipeline {
   stages {
       stage (' git checkout') {
           steps {
               checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Strvsuri/VALAXY-hello-world.git']])
           }
       }
   }
}
