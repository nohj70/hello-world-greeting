
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
        sh 'mvn -s $MAVEN_SETTINGS clean verify sonar:sonar -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER -Dsonar.host.url=http://172.17.0.1:9010'
    }
    
    
  }
  
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
    createTag nexusInstanceId: 'mi-server-repository-nexus-9080', tagAttributesJson: '{"createdBy" : "JohnSmith"}', tagName: 'tag-upload-p001'
    nexusPublisher nexusInstanceId: 'mi-server-repository-nexus-9080', nexusRepositoryId: 'maven-snapshots', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'target/hello-0.0.1.war']], mavenCoordinate: [artifactId: 'hello', groupId: 'employee', packaging: 'war', version: '0.0.1']]], tagName: 'tag-upload-p001'
    
    
  }
}
