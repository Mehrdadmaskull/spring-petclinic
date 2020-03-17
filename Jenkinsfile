pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './mvnw package'
        echo 'Building..'
        slackSend(color: '#000000', message: 'STARTED: Job is starting', baseUrl: 'https://hooks.slack.com/services/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', channel: 'jenkins-pipeline', teamDomain: 'pitchndine', username: 'incoming-webhook', tokenCredentialId: '9bb8ec72-7964-447b-85ba-a4a990c56f98')
        emailext(subject: 'STARTED: Job is starting', body: '''<p>STARTED: Job is starting:</p>
            <p>Check console output at &QUOT;<a href=\'http://localhost:9090/job/spring-petclinic/job\'></a>&QUOT;</p>''', to: 'm_hmadi@live.concordia.ca', recipientProviders: [[$class: 'CulpritsRecipientProvider'],[$class: 'RequesterRecipientProvider']])
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
      slackSend(color: '#000000', message: 'SUCCESSFUL: Job is built successfully')
      emailext(subject: 'SUCCESSFUL: Job is built successfully', body: '''<p>SUCCESSFUL: Job is built successfully:</p>
            <p>Check console output at &QUOT;<a href=\'http://localhost:9090/job/spring-petclinic/job\'></a>&QUOT;</p>''', to: 'm_hmadi@live.concordia.ca', recipientProviders: [[$class: 'CulpritsRecipientProvider'],[$class: 'RequesterRecipientProvider']])
    }

    failure {
      slackSend(color: '#000000', message: 'FAILED: Job failed to build')
      emailext(subject: 'FAILED: Job failed to build', body: '''<p>FAILED: Job failed to build:</p>
            <p>Check console output at &QUOT;<a href=\'http://localhost:9090/job/spring-petclinic/job\'></a>&QUOT;</p>''', to: 'm_hmadi@live.concordia.ca', recipientProviders: [[$class: 'CulpritsRecipientProvider'],[$class: 'RequesterRecipientProvider']])
    }

  }
}