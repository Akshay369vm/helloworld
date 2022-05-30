pipeline {
    agent any
    
    stages {
        stage('Cloning repo') {
            steps {
                git 'https://github.com/spring-petclinic/spring-framework-petclinic.git'           
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
