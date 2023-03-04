pipeline {
	agent { label 'JDK17' }
	options { 
		timeout(time: 1, unit: 'HOURS')
		retry(2)
	}
	triggers {
		cron('0 * * * *')
	}
	stages {
		stage('SourceCode') {
		steps {
			git url: 'https://github.com/cnukola/spring-petclinic.git', branch: 'main'
		}
		}
		stage('Buid the code') {
			steps {
				sh script: '/opt/apache-maven-3.8.7/bin/mvn clean package'
			}
		}
		stage('Reporting and Archiving') {
			steps {
				junit testResults: 'target/surefire-reports/*.xml'
			}
		}
	}
	post{
		success{
		echo "Sucess..........."
		}
		unsuccessful {
			echo "Failure ........"
		}
		}
}
