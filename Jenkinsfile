pipeline
{
   agent any
    stages
	{
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
      stage('test')
	    {
		steps
		    {
    			withCredentials([string(credentialsId: 'acc', variable: 'access')]) { //set SECRET with the credential content
        		//echo "My secret text is '${access}'"
				withCredentials([string(credentialsId: 'sec', variable: 'secr')]) { //set SECRET with the credential content
        			//echo "My secret text is '${secr}'"
					withCredentials([file(credentialsId: 'kp', variable: 'k_p')]) {
						withCredentials([file(credentialsId: 'kp2', variable: 'k_p2')]) {
				sh 'terraform init -no-color'
				sh 'terraform apply -auto-approve -no-color -var "acc=$access" -var "sec=$secr" -var "key_p=$k_p" -var "key_p2=$k_p2"'
			}
    		}
				}
			}
		}
	    }
	}
}
