node{

   def tomcatWeb = '/opt/apache-tomcat-9.0.43/webapps'
   def tomcatBin = '/opt/apache-tomcat-9.0.43/bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/jampa-rambabu/Dockerwebapp1.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'Maven', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
      sh "sudo cp  /var/lib/jenkins/workspace/pipelineTomcat/target/PersistentWebApp.war ${tomcatWeb}/"
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         sh "${tomcatBin}/startup.sh"
         sleep(time:100,unit:"SECONDS")
   }
}
