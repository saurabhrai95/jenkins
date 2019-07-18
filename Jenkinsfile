pipeline{
agent any



stages{

	
	stage('Checkout') {
		steps{
			
			bat '''
			java -version
			git clone https://github.com/saurabhrai95/read-service.git
			'''
		}
		
	
	}
	
	stage('Build'){
		steps{
			bat '''
			cd read-service
			mvn install
		'''
		}
	
	}
	
	stage('Sonarqube') {
		environment {
        scannerHome = tool 'SonarQubeScanner'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
            bat "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 1, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
	
	}
	
	
	
}

}
