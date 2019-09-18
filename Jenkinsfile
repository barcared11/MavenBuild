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
		sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000'
	}

	stage ('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}

	stage ('Deployment'){
		//sh 'cp target/*.war /opt/tomcat8/webapps'
	}
	
	stage ('Notification'){
		slackSend color: 'good', message: 'Successful Deployment'
		emailext(
			subject:'Jenkins Pipeline Success',
			body:'Pipeline deployment is a success go check your dashboard for more info.',
			to:'barcared11@gmail.com'
			)
	}
}
