pipeline {
  agent any

  environment{
        SCANNER_HOME= tool 'sonar-scanner'
  }  
  
  tools{
    maven 'maven3'
  }
  stages {
      stage('Checkout') {
            steps {
              git branch: 'main', credentialsId: '512fd7be-2f22-4c11-874c-9c20ac94d419', url: 'https://github.com/LSETProject2024/ecommerceservice.git'
            }
      }
      stage('Compile') {
            steps {
                sh 'mvn clean compile'
              }
      }
      stage('Test') {
            steps {
                sh 'mvn test'
            }
      }
      stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                sh 'mvn clean package sonar:sonar'
              }
            }
      }
      stage('SonarQube QualityGate'){
        steps {
                script {
                  waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token' 
                }
            }
      }
      stage('Build') {
            steps {
               sh "mvn package"
            }
        }
    
  }
}
