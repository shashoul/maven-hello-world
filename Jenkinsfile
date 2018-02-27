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
			parallel{
				stage('Deploy to Staging'){
                   steps{
                            sh "(cd my-app && scp -i ${env.JENKINS_HOME}/tomcat-demo.pem target/my-app-1.0-SNAPSHOT.jar shady@${params.tomcat_dev}:/var/lib/tomcat8/webapps) "
                         }
                }
				stage('Deploy to Producation'){
                   steps{
                            sh "(cd my-app && scp -i ${env.JENKINS_HOME}/tomcat-demo.pem target/my-app-1.0-SNAPSHOT.jar shady@${params.tomcat_prod}:/var/lib/tomcat8/webapps) "
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
