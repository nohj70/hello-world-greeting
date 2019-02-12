
node('build-ssh-slave-0.1') {
  stage('Poll') {
    sh 'git --version'
    sh 'java -version'
    checkout scm
  }
}
