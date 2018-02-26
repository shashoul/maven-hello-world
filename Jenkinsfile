pipeline {

	agent any 

	stages{
		stage("Build"){
		steps{
			sh "(cd my-app && mvn clean compile exec:java)"
	}
}
}
}
