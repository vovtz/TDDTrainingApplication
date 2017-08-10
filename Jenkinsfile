node {
   def mvnHome
   env.JAVA_HOME="${tool 'JDK 8'}"
   env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
   sh 'java -version'
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/vovtz/TDDTrainingApplication'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'Maven 3.3.9'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -f TDDTrainingApplicationCC/pom.xml -Dmaven.test.failure.ignore clean package"
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
}
