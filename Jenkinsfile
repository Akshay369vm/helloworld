pipeline {
    agent any
    
    stages {
        stage('Cloning repo') {
            steps {
                git 'https://github.com/Akshay369vm/simple-java-maven-app.git'            
            }
        }
        stage('maven build') {
              steps {
                  sh"""
                  cd $workspace
                  mvn clean package
                  cd target
                  ls -lrt
                  """
              }
         }
    }
}
