pipeline{

	agent any

	stages{

		stage("Test on Linux"){
			steps{
				sh "echo testing on Linux..."
			}
		}
		stage("Build"){
			agent{
				label 'linux-slave'
			}
			steps{
				sh "(cd my-app && mvn clean package)"
			}
		}
		stage("Run"){
			agent{
				label 'linux-slave'
			}
			steps{
				sh "(cd my-app && mvn exec:java)"	 					
 		    	sh "java -jar my-app/target/my-app-1.0-SNAPSHOT.jar"	
			}	 		
		}
		stage("Deployment"){
			agent{
				label 'linux-slave'
			}
			steps{
				sh "echo Deployment"
				}	
		}		
	}
}
