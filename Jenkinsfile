pipeline { 
  agent any
  tools { 
    nodejs "node-19"
  }
  stages { 
    stage('clone repository') {
      steps { 
        git 'https://github.com/ibrahimabdike/gallery.git'
      }
    }
    stage('Install Dependencies') {
      steps { 
        sh 'npm install'
      }
    }
    stage('Tests') {
      post{
        failure{
          mail bcc: '', body: 'Build Failed', cc: '', from: '', replyTo: '', subject: 'Build Failure', to: 'ibrahimabdike@gmail.com'
        }
      }
      steps { 
        sh 'npm test'
      }
    }
    stage('Slack Integration') {
      steps {
        slackSend channel: '#ibrahim_ip1', color: '#00FF00', message: "Build ${env.BUILD_NUMBER} has been Successful (<https://gallery-id7f.onrender.com|Open>)", teamDomain: 'devops-je18634', tokenCredentialId: 'slack'
      }
    }
    stage('Deploy on Render') {
      steps{
        withCredentials([usernameColonPassword(credentialsId: 'Render', variable: 'RenderCredentials')]) {
          sh 'git push https://api.render.com/deploy/srv-cgrc507dvk4n7bqjriog?key=qQRBOmbjg7o'
}
      }
    }
  }
}