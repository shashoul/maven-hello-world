pipeline {

	agent any 

	stages{
		
		stage("Build"){
		
			steps{
				sh "(cd my-app && mvn clean compile package exec:java)"
			}
		}

		stage("Jar"){
				steps{
					sh "java -jar target/my-app-1.0-SNAPSHOT.jar"
				}
			}
  }
}
