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
			parallel{
				stage("Deploy to Staging"){
					agent{
						label 'master'
					}
					options{
						skipDefaultCheckout()
					}
					steps{
						echo "Deploy to staging...."
						sh "scp -i ${env.JENKINS_HOME}/tomcat-demo.pem ${env.JENKINS_HOME}/jobs/${env.JOB_NAME}/lastSuccessful/archive/my-app/target/*.jar ${params.staging}:/var/lib/tomcat8/webapps "
					}
				}
				stage("Deploy to Production"){
					agent{
						label 'master'
					}
					options{
						skipDefaultCheckout()
					}
					steps{
						echo "Deploy to producation..."
						sh "scp -i ${env.JENKINS_HOME}/tomcat-demo.pem ${env.JENKINS_HOME}/jobs/${env.JOB_NAME}/lastSuccessful/archive/my-app/target/*.jar ${params.production}:/var/lib/tomcat8/webapps "
					}
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
