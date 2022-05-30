pipeline {
    agent any
    
    stages {
        stage('Cloning repo') {
            steps {
                git 'https://github.com/Akshay369vm/helloworld.git'
            }
        }
        stage('maven build') {
              steps {
                  sh"""
                  cd $workspace
                  mvn clean install
                  cd target
                  ls -lrt
                  """
              }
         }
    }
}
