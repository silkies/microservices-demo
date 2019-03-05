node("maven") {
	stage('Preparation') {
		git 'https://github.com/silkies/microservices-demo.git'
	}
	stage('Compile') {
		sh "mvn clean compile -Dtest=false -DfailIfNoTests=false"
	}
	stage('SonarQube') {
		sh "mvn sonar:sonar"
	}
	stage('Unit Tests') {
		sh "mvn clean test"
	}
	stage('Integration Tests') {
		sh "mvn clean verify -P integration-test"
	}
	stage('Build') {
		sh "mvn clean install -Dtest=false -DfailIfNoTests=false"
	}
	stage('Archive Artifacts') {
		archiveArtifacts '/*'
		archive 'target/*.jar'
	}
}
		
