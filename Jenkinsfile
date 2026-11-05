pipeline {
  agent any
  tools {
        jdk 'jdk17'
        maven 'MAVEN_HOME'
  }

  stages {
    stage('clone repository') {
      steps {
        bat '''java -version
            mvn --version
            git --version'''
      }
    }

    stage('Deploy billing App') {
      steps {
        withCredentials(bindings: [
                      string(credentialsId: 'kubernetes-jenkis-server-account', variable: 'api_token')
                      ]) {
            bat 'kubectl --token %api_token% --server https://127.0.0.1:64770 --insecure-skip-tls-verify=true apply -f deployment-billing-app-back-jenkins.yaml --validate=false'
          }

        }
      }

    }
  }