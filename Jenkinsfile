myVar = 'initial_value'
node {
  stage('Poll') {
    echo 'Staging Components...'
    echo "1: ${myVar}" // prints 'hotness'
    echo "2"
    echo myVar
    echo "3"
    
    checkout scm
    
    pom = readMavenPom file: 'pom.xml'
    echo pom.version
  }
  
  
  stage('stge 2') {
    echo 'stge 2...'
    echo "4: ${myVar}" // prints 'hotness'
    echo "5"
    echo myVar
    echo "6"
  }
}
