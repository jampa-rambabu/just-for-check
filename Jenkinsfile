pipeline
{
    agent any
	environment{
        PATH = "/opt/maven/apache-maven-3.6.3/bin:$PATH"
	}
    stages
	{
	stage("SCM Checkout"){
            steps{
               git credentialsId: '3dd0fa55-769d-4326-af17-46c823c096ee', url: 'https://github.com/jampa-rambabu/Dockerwebapp1.git'
        }
    }
    stage("Compile A Pacakge"){
        steps{
            sh "mvn package"
        }
    }
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