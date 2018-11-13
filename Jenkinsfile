#!groovy
import jenkins.model.*

pipeline {
    agent any
    options {
      buildDiscarder(logRotator(numToKeepStr: '7'))
      timeout(time: 10, unit: 'MINUTES')
    }
    stages{
        stage('Stage 1'){
            echo 'Stage 1'
        }
        stage('Stage 2'){
            echo 'Stage 2'
        }
    }
}