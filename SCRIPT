# jenkinspipeline
node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
    //  git 'https://github.com/ramyeldutiggk/java-app.git'
     def scmUrl = scm.getUserRemoteConfigs()[0].getUrl()
     //def url = sh(returnStdout: true, script: 'git config remote.origin.url').trim()
     git scmUrl
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
        dir('SpringMVCSecurityXML') {
            sh 'pwd'
    // some block
         if (isUnix()) {
             
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
        }
      }
      input "approve?"
   }
   stage('Results') {
     
      archiveArtifacts '**/target/*.war'
   }
   stage('Deploy'){
      
    sh 'cp SpringMVCSecurityXML/target/SpringMVCSecurityXML.war /opt/tomcat/apache-tomcat-9.0.20/webapps/javapipeline.war'

   }
   
}

