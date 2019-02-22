
AGENT_LABEL_PRD = "none"
AGENT_LABEL_ACCEPTANCE = "none"
AGENT_LABEL = "none"

node('aget-ssh-9094-1') {
  stage('Poll') {
    sh 'git --version'
    //if (true) {
      
      
        AGENT_LABEL_ACCEPTANCE = "docker-performance-testing"      
        AGENT_LABEL_PRD = "docker-prd"
        AGENT_LABEL = "docker-performance-testing"
     //}
  }
}


pipeline {
    agent {
       label "$AGENT_LABEL"
    }

    stages {
        stage('deployment') {
           steps {
              echo "deployment in ${AGENT_LABEL}"
              echo "Running in ${AGENT_LABEL}"
           }
        }
    }
}

