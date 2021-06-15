node('master') {
  ansiColor('xterm') {
	stage ('checkout code'){
		checkout scm
	}
	
	
	stage ('Build'){
		sh "mvn clean install -Dmaven.test.skip=true"
	}
	
   }
}


node('slave1') {
	ansiColor('xterm') {
	  
	  stage ('Test Cases Execution'){
		  sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
	  }
  	
	 }
  }
  

  node('slave2') {
	ansiColor('xterm') {
	  
		stage ('Archive Artifacts'){
			archiveArtifacts artifacts: 'target/*.war'
		}
  	
		stage ('Notification'){
			//slackSend color: 'good', message: 'Deployment Sucessful'
			emailext (
				  subject: "Job Completed",
				  body: "Jenkins Pipeline Job for Maven Build got completed !!!",
				  to: "monther.g.07@gmail.com"
				)
		}
	 }
  }
