pipeline{

	parameters{
		string(name:"build_machine_lable",defaultValue:"linux-slave",description:"the linux build machine label name")
        string(name:"tomcat_dev",defaultValue:'10.64.106.246',description:'Staging Server')
        string(name:"tomcat_prod",defaultValue:'10.64.107.249',description:'Production Server')
    }

	agent{
		label "'${params.build_machine_lable}'"
		}

	stages{
		stage("Test on Linux Machine"){
			steps{
				sh "echo test on Linux machine..."
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
		stage("Deployment"){
			steps{
				sh "echo Deployment"
				}	
		}		
	}

	post{
		success{
			sh "echo ${env.JENKINS_HOME} ${env.JENKINS_USER}"
			sh "echo Build is success!!!"
		}
		failure {
			sh "echo Build failed!!!"
		}
	}

}
