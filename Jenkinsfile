
AGENT_LABEL_PRD = none
AGENT_LABEL_ACCEPTANCE = none

node('aget-ssh-9094-1') {
  stage('Poll') {
    sh 'git --version'
    //if (true) {
      
      
        //AGENT_LABEL_ACCEPTANCE = "docker-performance-testing"      
        AGENT_LABEL_PRD = "docker-prd"
     //}
  }
}


pipeline {
    agent {
       label $AGENT_LABEL_PRD
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
             label $AGENT_LABEL_ACCEPTANCE
            }
            steps{
              echo "stage Prd build"
              echo "Running in ${AGENT_LABEL_ACCEPTANCE}"
            }
        }
    }
}

