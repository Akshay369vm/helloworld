pipeline {
    agent any
    
    stages {
        stage('Cloning repo') {
            steps {
                git ' https://github.com/daticahealth/java-tomcat-maven-example.git'           
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
        stage('deploy') {
            steps { 
                sh """ cp target/java-tomcat-maven-example.war /opt/tomcat/webapps/
                       sudo systemctl restart tomcat"""
            }
    }
}
