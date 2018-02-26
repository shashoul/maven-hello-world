pipeline {

	agent any 

	stages{
		
		stage("Build"){
		
			steps{
				sh "(cd my-app && mvn clean compile exec:java)"
			}
		
			stage("Jar"){
				sh "java -jar my-app/target/my-app-1.0-SNAPSHOT.jar"
			}
		}
  }
}
