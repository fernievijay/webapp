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
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@18.224.190.133:/opt/tomcat/webapps/webapp.war'
              }      
           }       
    }
  }
}
