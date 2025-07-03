pipeline{
    agent any
     tools {
        sonarQubeScanner 'sonarqube' // Replace with your SonarQube Scanner tool name
    }
       environment {
        
        SONARQUBE_ENV = 'sonarqube' // Replace with your SonarQube server name from Jenkins settings
    }
    stages{
        stage("git cheackout"){
            steps{
                    git branch: 'main', url: 'https://github.com/KARTIKNAIK18/Bingo-k8s.git'
            }
        }
        stage("Sonarqube analysis"){
            steps{
                withSonarQubeEnv("${SONARQUBE_ENV}"){
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage("Quality Gate"){
            steps{
                timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
        }

    }
}
