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
   stage('Results') {
       archiveArtifacts 'target/*.jar'
       junit 'target/surefire-reports/*.xml'
       step([$class: 'ElectricFlowPipelinePublisher', 
           configuration: 'local',
           projectName  : 'CloudBees',
           pipelineName : 'TestPipeline',
           addParam     : ''
       ])
        
   }
}
