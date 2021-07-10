pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build Demo App'
      }
    }

    stage('Linux Tests') {
      parallel {
        stage('Linux Tests') {
          steps {
            echo 'Run Linux tests'
          }
        }

        stage('Window Tests') {
          steps {
            echo 'Run Windows Tests'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        echo 'Deploy to Staging environment'
        input 'Ok to deploy to Production?'
      }
    }

    stage('Deploy Production') {
      post {
        always {
          archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
        }

        failure {
          mail(to: 'ashok.m.mane@gmail.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
        }

      }
      steps {
        echo 'Deploy to Production'
      }
    }

  }
}