node('master') {

	stage ('checkout code'){
		checkout scm
	}

	stage ('Build'){
		sh "mvn clean install"
	}

	stage ('Test Cases Execution'){
		sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
	}

	stage ('Sonar Analysis'){
		//sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:80'
	}

	stage ('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}

	stage ('Deployment'){
		// sh 'cp target/*.war /opt/tomcat8/webapps'
	}
	
	stage ('Notification'){
		slackSend color: 'good', message: 'Deployment Success'
		emailext (
		      subject: "Job Completed",
		      body: "Jenkins Pipeline Job for Maven Build got completed !!!",
		      to: "anuj_sharma401@yahoo.com"
		    )			
	}
}
