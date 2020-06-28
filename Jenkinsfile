// Declarative syntax - More modern and results in a declarative pipeline

pipeline {
		agent any
		//agent { docker { image 'maven:3.6.3'}} # Any docker image can be built here
		environment {
				dockerHome = tool 'myDocker'
				mavenHome = tool 'myMaven'
				PATH = "$mavenHome/bin:$dockerHome/bin:$PATH"

		}
		stages {
			stage('Checkout') {
				steps {
						
						// echo "Build"
						sh 'mvn --version'
						sh 'docker version'
						echo "PATH - $PATH"
						echo "BUILD_NUMBER - $env.BUILD_NUMBER"
						echo "BUILD_ID - $env.BUILD_ID"
						echo "BUILD_TAG - $env.BUILD_TAG"
						echo "BUILD_URL - $env.BUILD_URL"
						echo "JOB_NAME - $env.JOB_NAME"
				}
			}
			stage('Compile') {
				steps {
						sh "mvn clean compile"
				}
			}	
			stage('Test') {
				steps {
						sh "mvn test"
				}
			}	
			stage('Integration Test') {
			steps {
					sh "mvn failsafe:integration-test failsafe:verify"
			    }
			}
			stage('Package') {
			steps {
					sh "mvn package -DskipTests"
			    }
			}
			stage('Build Docker Image') {
			steps {
					//"docker build -t soodipop/currency-exchange-jenkins:$env.BUILD_TAG" #old school way of doing it
					// New way of doing it
					script{ 
						dockerImage = docker.build("soodipop/currency-exchange-jenkins:${env.BUILD_TAG}")
					}
			    }
			}
			stage('Push Docker Image') {
			steps {
					script{
						dockerwithRegistry('', 'dockerhub') {
							dockerImage.push();
							dockImage.push('latest');
						}
					}
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