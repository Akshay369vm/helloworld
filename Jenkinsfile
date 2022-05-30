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
                  script {
                      sh"""
                      cd $workspace
                      ./mvnw clean install
                      cd target
                      ls -lrt
                      """
                  }
              }
         }
    }
}
