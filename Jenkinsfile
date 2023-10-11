pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '13.232.37.20', description: 'Remote Staging Server')
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    stage('Deploy to Tomcat server'){
      steps{
        deploy adapters: [tomcat9(credentialsId: 'tomcat_deployer', path: '', url: 'http://13.126.87.140:8080/')], contextPath: null, war: '**/*.war'
      }
      
    }
  }
}
