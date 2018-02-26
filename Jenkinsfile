pipeline {

	agent any 

	stages{
		
		stage("Build"){
		
			steps{
				sh "(cd my-app && mvn clean package exec:java)"
			}
		}

		stage("Jar"){
				steps{
					sh "(cd my-app && mvn exec:java)"
					sh "java -jar my-app/target/my-app-1.0-SNAPSHOT.jar"
				}
			}

		stage("Deployment"){
				steps{
					sh "echo deplyment"
				}
		}
		
  }
}
