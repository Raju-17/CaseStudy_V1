node {
   def mvnHome
   stage('Checkout') { // for display purposes
      // Get some code from a GitHub repository
      //checkout([$class: 'GitSCM', doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '6f8af427-afa3-4493-b0d3-6948b22eb355', 
                                    // url: 'https://github.com/Raju-17/CaseStudy_V1.git']]])
       git 'https://github.com/Raju-17/CaseStudy_V1.git'
      // Get the Maven tool.
      // ** NOTE: This 'maven-3.6.1' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'maven-3.6.1'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
   
  stage('sonar-qube') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore sonar:soanr -Dsonar.host.url='http://ec2-13-233-157-115.ap-south-1.compute.amazonaws.com:9000/'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore sonar:soanr -Dsonar.host.url='http://ec2-13-233-157-115.ap-south-1.compute.amazonaws.com:9000/')
         }
      }
   }
}
