pipeline {
    agent any
    
    stages {
        stage('Cloning repo') {
            steps {
                git ' https://github.com/daticahealth/java-tomcat-maven-example.git'           
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SCANNER_HOME = tool 'SonarQube'
                //ORGANIZATION = "AkshayVM"
                PROJECT_NAME = "petclinic-tomcat"
            }
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                        sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=$PROJECT_NAME \
                        -Dsonar.java.binaries=\"target/classes/\"'''
                    }
                }
            }
        }
        stage("Quality gate") {
            steps {
                script {
                    def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            sh "exit 1"
                        }
                }
                waitForQualityGate abortPipeline: true
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
                sh """ sudo cp target/java-tomcat-maven-example.war /opt/tomcat/webapps/
                       sudo systemctl restart tomcat"""
            }
        }
    }
}
