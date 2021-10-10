node {

    def mvnHome = tool 'Maven3'
    stage ("checkout")  {
     //enter your repo info
    }

     stage ('Build')  {
        sh "${mvnHome}/bin/mvn -f MyWebApp/pom.xml clean install"
   }
     stage ('Code Quality scan')  {
       withSonarQubeEnv('SonarQube') {
        sh "${mvnHome}/bin/mvn -f MyWebApp/pom.xml sonar:sonar"
        }
   }
   
     stage("Quality Gate") {
        timeout(time: 1, unit: 'HOURS') {
            waitForQualityGate abortPipeline: true
        }
  }       
}
