pipeline {
  agent any
  node {
    checkout scm
  }
  stages {
    stage('download warfile') {
      steps {
        sh '''#!/bin/bash
            echo 'Starting to download warfile '
            curl -o sample.war https://tomcat.apache.org/tomcat-8.0-doc/appdev/sample/sample.war
         '''
      }
    }
    stage('Build image') {
      steps {
        echo 'Starting to build docker image'

        script {
          def customImage = docker.build("hub.docker.com/ashwajce/sample-app:${env.BUILD_ID}")
          customImage.push()
        }
      }
    }
  }
}
