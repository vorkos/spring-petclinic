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
                script { test 'test'}
            }
        }
        stage('Run via maven') {
            steps {
                script {sonarScan()}
            }
        }
        stage("SonarQube quality gate") {
            steps {
                script {
                    sonarCLI{
                        serviceName = "localhost"
                    }
                }
            }
        }
    }
}