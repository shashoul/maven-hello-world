pipeline{

	agent {
			label 'linux-slave'
		} 

	stages{

		stage("Build"){
			steps{
				sh "(cd my-app && mvn clean package)"
			}
		}

		stage("Run"){
			steps{	 		
 					sh "(cd my-app && mvn exec:java)"	 					
 					sh "java -jar my-app/target/my-app-1.0-SNAPSHOT.jar"	 				
 				}
		}

		stage("Deployment"){
			steps{
				sh "echo Deployment"
			}
		}

	}
}