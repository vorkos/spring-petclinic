#!groovy
import jenkins.model.*

pipeline {
    agent any
    options {
      buildDiscarder(logRotator(numToKeepStr: '7'))
      timeout(time: 10, unit: 'MINUTES')
    }
    stages{
        stage('debug') {
            steps {
                echo 'Debug info'
                sh(returnStdout: true, script: """
                ls -la ${pwd()}
                """)
            }
        }
        stage('Run via maven') {
            steps {
                withSonarQubeEnv('sonarqube') {
                        sh 'mvn clean package sonar:sonar'
                  	}
            }
        }
        stage("SonarQube quality gate") {
            steps {
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}