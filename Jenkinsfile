pipeline {
  agent any
  tools {
    maven "Maven"
  }
  stages {
    stage ('initialize') {
      steps {
        sh '''
              echo "PATH = $(PATH)"
              echo "M2_HOME = $(M2_HOME)"
           '''   
        
      }
    }
    
    stage ('build') {
      steps {
        sh 'mvn clean package'
      }
    }
    
    stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@54.157.226.232:/opt/tomcat/webapps/webapp.war'
              }      
           }       
    }
  }
}
