pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build Demo App'
        bat 'call build.bat'
      }
    }

    stage('Linux Tests') {
      parallel {
        stage('Linux Tests') {
          steps {
            echo 'Run Linux tests'
            bat 'call test1.bat'
          }
        }

        stage('Window Tests') {
          steps {
            echo 'Run Windows Tests'
            bat 'call test2.bat'
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