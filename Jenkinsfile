#!groovy
import jenkins.model.*
@Library('test')_


pipeline {
    agent any
    options {
      buildDiscarder(logRotator(numToKeepStr: '7'))
      timeout(time: 20, unit: 'MINUTES')
    }
    stages{
        stage('debug') {
            steps {
                test 'test'
                sh(returnStdout: true, script: """
                ls -la ${pwd()}
                """)
            }
        }
        stage('Run via maven') {
            steps {
                sonarScan()
            }
        }
        stage("SonarQube quality gate") {
            steps {
                timeout(time: 20, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}