node("maven") {
	stage('Preparation') {
		git 'https://github.com/silkies/microservices-demo.git'
	}
	stage('Compile') {
		sh "mvn clean compile -Dtest=false -DfailIfNoTests=false"
	}
	stage('SonarQube') {
		withSonarQubeEnv('MySonarQubeServer') {
      			sh "mvn sonar:sonar"
    		}
	}
	stage('Unit Tests') {
		sh "mvn clean test"
	}
	stage('Integration Tests') {
		sh "mvn verify"
	}
	stage('Build') {
		sh "mvn install -Dtest=false -DfailIfNoTests=false"
	}
	stage('Archive Artifacts') {
		archiveArtifacts '/*'
		archive 'target/*.jar'
	}
}
		
