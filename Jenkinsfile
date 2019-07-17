pipeline{
agent any
tools{
	maven 'apache-maven'
	jdk 'jdk1.8'
}


stages{

	
	stage('Checkout') {
		steps{
			bat '''
			echo "JAVA_HOME = ${JAVA_HOME}"
			echo "M2_HOME = ${M2_HOME}"
			echo "Checkout from git"
			git clone https://github.com/saurabhrai95/read-service.git
			'''
		}
	
	}
	stage('Sonarqube') {
		environment {
        scannerHome = tool 'SonarQubeScanner'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 1, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
	
	}
	
	stage('Build') {
		steps{
			bat '''
			echo "Build and Unit Test"
			'''
		
		}
	
	}
	
	
}

}
