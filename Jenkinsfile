pipeline {
    agent any
    
    tools {maven "Maven386"}
    
    environment {
        SONAR_TOKEN = credentials('global-sonar-token')
        DOJO_TOKEN = credentials('global-dojo-token')
    }

    stages {
        stage('Clone sources') {
            steps {
                git branch: 'main', credentialsId: 'my-credential', url: 'https://github.com/global-develop-qa/java-maven.git'
            }
        }
      

          
    }
}
