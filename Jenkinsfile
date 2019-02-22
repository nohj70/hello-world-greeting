
AGENT_LABEL = null

node('aget-ssh-9094-1') {
  stage('Poll') {
    sh 'git --version'
    if (true) {
        AGENT_LABEL = "docker-prd"
     }
  }
}


pipeline {
    agent {
       label "docker-performance-testing"
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
             label "${AGENT_LABEL}"
            }
            steps{
              echo "stage Prd build"
              echo "Running in ${AGENT_LABEL}"
            }
        }
    }
}

