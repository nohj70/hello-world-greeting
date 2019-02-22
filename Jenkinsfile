
myVar='asdf'

node('aget-ssh-9094-1') {
  stage('Poll') {
    scm checkout
    
    //versionPom = readMavenPom().getVersion()
    
     echo "${myVar}"
  }
}
