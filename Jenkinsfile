import jenkins.model.*
jenkins = Jenkins.instance

node('build-ssh-slave-0.1') {
  stage('Poll') {
    scm checkout
  }
}
