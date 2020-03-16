pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh './mvnw package'
        echo 'Building..'
        
        // send slack notification
        slackSend (color: '#000000', message: "STARTED: Job is starting")

        // send to email
        emailext (
          subject: "STARTED: Job is starting",
          body: """<p>STARTED: Job is starting:</p>
            <p>Check console output at &QUOT;<a href='http://localhost:9090/job/spring-petclinic/job'></a>&QUOT;</p>""",
          recipientProviders: ["m_hmadi@live.concordia.ca"]]
        )
      }
    }
    stage('Test') {
      steps {
          echo 'Testing..'
      }
    }
    stage('Deploy') {
      steps {
          echo 'Deploying....'
      }
    }
  }

  post {
    success {
      // send slack notification
        slackSend (color: '#000000', message: "SUCCESSFUL: Job is built successfully")

        // send to email
        emailext (
          subject: "SUCCESSFUL: Job is built successfully",
          body: """<p>SUCCESSFUL: Job is built successfully:</p>
            <p>Check console output at &QUOT;<a href='http://localhost:9090/job/spring-petclinic/job'></a>&QUOT;</p>""",
          recipientProviders: ["m_hmadi@live.concordia.ca"]]
        )
    }

    failure {
      // send slack notification
        slackSend (color: '#000000', message: "FAILED: Job failed to build")

        // send to email
        emailext (
          subject: "FAILED: Job failed to build",
          body: """<p>FAILED: Job failed to build:</p>
            <p>Check console output at &QUOT;<a href='http://localhost:9090/job/spring-petclinic/job'></a>&QUOT;</p>""",
          recipientProviders: ["m_hmadi@live.concordia.ca"]]
        )
    }
  }
}