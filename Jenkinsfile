
myVar='asdf'

node('aget-ssh-9094-1') {
  stage('Poll') {
    scm checkout
    
    some_var = 'Hello World' // this is Groovy
    echo some_var // printing via Groovy works
    sh "echo $some_var"
  }
}
