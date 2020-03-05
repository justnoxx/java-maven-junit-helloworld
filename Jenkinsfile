node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/justnoxx/java-maven-junit-helloworld.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'mvn'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
          sh '"$MVN_HOME/bin/mvn" install'
      }
   }
   stage('Publish') {
       cloudBeesFlowPublishArtifact artifactName: 'com.example:java-maven-junit-helloworld', artifactVersion: '2.0-SNAPSHOT', configuration: 'docker1', filePath: 'target/java-maven-junit-helloworld-2.0-SNAPSHOT.jar', repositoryName: 'default'
   }
   stage('Results') {
       archiveArtifacts 'target/*.jar'
       junit 'target/surefire-reports/*.xml'
       cloudBeesFlowRunPipeline addParam: '{"pipeline":{"pipelineName":"DmitriysPipeline","parameters":[]}}', configuration: 'docker1', pipelineName: 'DmitriysPipeline', projectName: 'Default'
   }
}
