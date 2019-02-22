
def isSnapshot = false

node('aget-ssh-9094-1') {
  stage('Poll') {
    scm checkout
    
    echo "version pom: $readMavenPom().getVersion()"
  }
}
