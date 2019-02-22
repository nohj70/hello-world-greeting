myVar = 'initial_value'
node('aget-ssh-9094-1') {
  stage('Poll') {
    echo 'Staging Components...'
    echo "1: ${myVar}" // prints 'hotness'
    echo "2"
    echo myVar
    echo "3"
    
    scm checkout
    
    echo 'Staging Components...'
    echo "4: ${myVar}" // prints 'hotness'
    echo "5"
    echo myVar
    echo "6"
  }
}
