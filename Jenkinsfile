pipeline {
  agent any
  options { timestamps() }
  triggers { pollSCM('H/5 * * * *') }
  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/lina769/tp2.git', branch: 'main'
      }
    }
    stage('Build') {
      steps {
        bat 'echo === Build : verification des fichiers ==='
        bat 'dir'
        bat 'if not exist *.html exit 1'
        bat 'if not exist *.css exit 1'
      }
    }
    stage('Test') {
      steps {
        bat 'echo === Test : le HTML contient un titre h1 ==='
        bat 'findstr /i "<h1>" *.html'
      }
    }
    stage('Delivery') {
      steps {
        bat 'echo === Delivery : copie vers le dossier de livraison ==='
        bat 'if not exist C:\\DevOps\\delivery mkdir C:\\DevOps\\delivery'
        bat 'copy *.html C:\\DevOps\\delivery /Y'
        bat 'copy *.css C:\\DevOps\\delivery /Y'
        archiveArtifacts artifacts: '**/*.html, **/*.css', fingerprint: true
      }
    }
  }
  post {
    success { echo 'Build OK' }
    failure { echo 'Build KO' }
  }
}
