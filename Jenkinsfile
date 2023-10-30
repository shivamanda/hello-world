pipeline {
    agent any
    
    tools {
        maven 'Maven3.9.5'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '172.31.36.208', description: 'Remote Staging Server')
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
        deploy adapters: [tomcat9(credentialsId: 'tomcat_deployer', path: '', url: 'http://3.109.144.222:8080/')], contextPath: null, war: '**/*.war'
      }
      
    }
  }
}
