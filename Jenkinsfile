node('master') {
	ansiColor('xterm') {
		node('slave1'){
			stage ('checkout code'){
				checkout scm
			}

			stage ('Build'){
				sh "mvn clean install -Dmaven.test.skip=true"
			}

			stage ('Test Cases Execution'){
				sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
			}

			stage ('Archive Artifacts'){
				archiveArtifacts artifacts: 'target/*.war'
			}
		}

		node('slave2'){
			stage ('checkout code'){
				checkout scm
			}

			stage ('Build on slave nodes'){
				sh "mvn clean install -Dmaven.test.skip=true"
			}

			stage ('Test Cases Execution'){
				sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
			}

			stage ('Archive Artifacts'){
				archiveArtifacts artifacts: 'target/*.war'
			}
		}

		stage ('Deployment'){
		
		}
		stage ('Notification'){
			//slackSend color: 'good', message: 'Deployment Sucessful'
			emailext (
				subject: "Job Completed",
				body: "Jenkins Pipeline Job for Maven Build got completed !!!",
				to: "ialqwaiz@gmail.com"
			)
		}
   }
}
