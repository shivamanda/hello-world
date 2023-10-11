pipeline{
  node any
  stages{
    stage('Build'){
      steps{
        sh 'mvn clean package'
      }
      post{
        echo 'archiving artofacts'
        archiveArtifacts artifacts: '**/target/*.war'
      }
      
    }
    stage('Deploy to Tomcat server'){
      steps{
        deploy adapters: [tomcat9(credentialsId: 'tomcat_deployer', path: '', url: 'http://13.126.87.140:8080/')], contextPath: null, war: '**/*.war'
      }
      
    }
  }
}
