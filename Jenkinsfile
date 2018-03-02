pipeline{

	parameters{
		string(name:"build_machine_label",defaultValue:"master",description:"the linux build machine label name")
        string(name:"staging",defaultValue:'shady@10.64.106.246',description:'Staging Server')
        string(name:"production",defaultValue:'shady@10.64.107.249',description:'Production Server')
    }

	agent{
		label "'${params.build_machine_label}'"
		}

	stages{
		stage("Linux"){
			steps{
				sh "echo build running on Linux machine label '>>>' ${params.build_machine_label}"
			}
		}
		stage("Build"){
			steps{
				sh "(cd my-app && mvn clean package)"
			}
		}
		stage("Running"){
			steps{
 		    	sh "(cd my-app && java -jar target/my-app-1.0-SNAPSHOT.jar)"	
			}	 		
		}
		stage("Archive"){
			steps{
				echo "Archiving..."
                archiveArtifacts artifacts: '**/target/*.jar' 
			}
		}
		stage("Deployment"){
			agent{
				label 'master'
			}
			options{
				skipDefaultCheckout()
			}
			parallel{
				stage("Deploy to Staging"){
					echo "deploy ot staging...."
				}
				stage("Deploy to Production"){
					echo "deploy to producation..."
				}
			}
		}
	}

	post{
		success{
			sh "echo Build is success!!!"
		}
		failure {
			sh "echo Build failed!!!"
		}
	}
}
