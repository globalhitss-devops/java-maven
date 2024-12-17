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

      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' 
            }  
       }
        
      stage('Test Maven - JUnit') {
            steps {
              sh "mvn test"
            }
            post{
              always{
                junit 'target/surefire-reports/*.xml'
              }
            }
        }
        
        stage("SonarQube Analysis"){
            environment {
                SCANNER_HOME = tool 'SonarQubeScanner';    
            }

            steps{
               withSonarQubeEnv("SonarQube"){
                   sh '''mvn sonar:sonar \
                   -Dsonar.projectName=java-maven \
                   -Dsonar.projectKey=java-maven \
                   -Dsonar.sources=. '''
               }
            }
        }
        
    }
}
