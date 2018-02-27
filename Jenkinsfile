pipeline{

	agent any

	stages{

		stage("Linux"){
			
			node('linux-slave'){
					stage("Build"){
						
						sh "(cd my-app && mvn clean package)"
						
					}
					stage("Run"){
							 		
 							sh "(cd my-app && mvn exec:java)"	 					
 							sh "java -jar my-app/target/my-app-1.0-SNAPSHOT.jar"	 				
 						
					}
					stage("Deployment"){
						
							sh "echo Deployment"
						
					}	
			}
			
		}
		
	}
}