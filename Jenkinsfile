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
      steps { 
        sh 'npm test'
      }
    }
  }
}