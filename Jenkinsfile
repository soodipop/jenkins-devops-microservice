// Declarative syntax - More modern and results in a declarative pipeline

pipeline {
		//agent any
		agent { docker { image 'maven:3.6.3'}}
		stages {
			stage('Build') {
				steps {
						
						echo "Build"
						sh 'mvn --version'
				}
			}
			stage('Test') {
				steps {
						echo "Test"
				}
			}	
			stage('Integration Test') {
			steps {
					echo "Integration Test"	
			    }
			}

		} 
		post {
			always{
				echo 'Im awesome, I run always'
			}

			success{
				echo 'I run when you are successful'
			}
			 
			failure{
				echo 'Im awesome, I run always'
			}

			//unstable
			//changed -- status change between buildsin the builds list

		}

		
}


/* Scripted syntax (Old way of writing a Jenkins file) and results in a scripted pipeline*/
/*
node {

		stage('build') {
			echo "build"
		}
		
		stage('test') {
			echo "test"
		}

		stage('integration test') {
			echo "integration test"
		}

}


*/


// This is also legit scripting syntax
/*

node{

	echo "Build"
	echo "Test"
	echo "Integration Test"

}

*/