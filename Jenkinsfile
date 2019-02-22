
AGENT_LABEL_PRD = null
AGENT_LABEL_ACCEPTANCE = null

node('aget-ssh-9094-1') {
  stage('Poll') {
    sh 'git --version'
    //if (true) {
      
      
        AGENT_LABEL_ACCEPTANCE = "docker-performance-testing"      
        //AGENT_LABEL_PRD = "docker-prd"
     //}
  }
}


pipeline {
    agent {
       label none
    }

    stages {
        stage('Prd build') {
           steps {
              echo "stage Performance build"
              echo "Running in ${AGENT_LABEL}"
           }
        } 

        stage ("Performance build") {
           agent{             
             label none
            }
            steps{
              echo "stage Prd build"
              echo "Running in ${AGENT_LABEL_ACCEPTANCE}"
            }
        }
    }
}

