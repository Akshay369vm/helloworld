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
                //waitForQualityGate abortPipeline: true
                timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
                def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
                if (qg.status != 'OK') {
                error "Pipeline aborted due to quality gate failure: ${qg.status}"
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
