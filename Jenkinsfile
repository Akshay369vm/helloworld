pipeline {
    agent any
    
    stages {
        stage('Cloning repo') {
            steps {
                git 'https://github.com/Akshay369vm/helloworld.git'
            }
        }
        stage("maven build') {
              step {
                  script {
                      sh"""
                      cd $workspace/maven-project
                      mvn clean install
                      cd target
                      ls -lrt
                      """
                  }
              }
         }
    }
}
