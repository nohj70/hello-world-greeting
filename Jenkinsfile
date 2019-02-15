
node('aget-ssh-9094-1') {
  stage('Poll') {
    
    checkout scm
    
    configFileProvider(
        [configFile(fileId: '0bb82d12-668b-40a8-9d96-61f1d04a243f', variable: 'MAVEN_SETTINGS')]) {
        sh 'mvn -s $MAVEN_SETTINGS clean'
    }
  }
  
  stage('Build & Unit test') {
    
    configFileProvider(
        [configFile(fileId: '0bb82d12-668b-40a8-9d96-61f1d04a243f', variable: 'MAVEN_SETTINGS')]) {
        sh 'mvn -s $MAVEN_SETTINGS clean verify -DskipITs=true'
    }
    
    
    junit '**/target/surefire-reports/TEST-*.xml'
    
    archiveArtifacts 'target/*.war'
  }
  
  stage('Static Code Analysis') {
    
    configFileProvider(
        [configFile(fileId: '0bb82d12-668b-40a8-9d96-61f1d04a243f', variable: 'MAVEN_SETTINGS')]) {
      
      withSonarQubeEnv('mi-sonar-9010') {
          sh 'mvn -s $MAVEN_SETTINGS clean verify sonar:sonar -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER -Dsonar.host.url=http://172.17.0.1:9010'
      } // SonarQube taskId is automatically attached to the pipeline context
      
      timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
        def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
        
        echo "Result quality gate: ${qg}"
        
        if (qg.status != 'OK') {
          error "Pipeline aborted due to quality gate failure: ${qg.status}"
        }
      }
    
    
    }//end configFileProvider
    
    
  }//end stage Static Code Analysis
  
  stage('Integration Test'){
    
    configFileProvider(
        [configFile(fileId: '0bb82d12-668b-40a8-9d96-61f1d04a243f', variable: 'MAVEN_SETTINGS')]) {
        sh 'mvn -s $MAVEN_SETTINGS clean verify -Dsurefire.skip=true'
    }
    
    junit '**/target/failsafe-reports/TEST-*.xml'
    
    archiveArtifacts 'target/*.war'
  }
  
  stage ('Publish'){
    /*
    def server = Artifactory.server 'Default Artifactory Server'
    def uploadSpec = """{
      "files": [
        {
          "pattern": "target/hello-0.0.1.war",
          "target": "example-project/${BUILD_NUMBER}/"
          "props": "Integration-Tested=Yes;Performance-Tested=No"
        }
      ]
    }"""
    server.upload(uploadSpec)
    */
    
    
    nexusPublisher nexusInstanceId: 'mi-server-repository-nexus-9080', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/hello-0.0.1.war']], mavenCoordinate: [artifactId: 'hello', groupId: 'employee', packaging: 'war', version: '0.0.$BUILD_NUMBER']]]
    
stash includes:
  'target/hello-0.0.1.war,src/pt/plan-prueba-001.jmx',
  name: 'binary'


    
  } 
  
  
}


node('docker-performance-testing'){
  stage('stage iniciando tomcat'){
    sh '''cd /opt/tomcat/bin
      ./startup.sh''';
  }
  
  stage('despliegue'){
    unstash 'binary'
    sh 'cp target/hello-0.0.1.war /opt/tomcat/webapps/';
    
  }
  
  stage('performance testing'){
    
    sh '''cd /opt/jmeter/bin/
    ./jmeter.sh -n -t $WORKSPACE/src/pt/plan-prueba-001.jmx -l $WORKSPACE/test_report.jtl''';
    
    step([$class: 'ArtifactArchiver', artifacts: '**/*.jtl'])
    
  }

}




















