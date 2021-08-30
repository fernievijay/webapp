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
    stage ('check secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run dxa4481/trufflehog --json https://github.com/fernievijay/webapp.git > trufflehog'
        sh 'cat trufflehog'
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
