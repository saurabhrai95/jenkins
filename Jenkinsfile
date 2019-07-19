pipeline{
agent any

tools {
  maven 'apache-maven'
  jdk 'jdk1.8'
}



stages{

	
	stage('Checkout') {
		steps{
			git(url: 'https://github.com/saurabhrai95/read-service.git', branch: 'master', changelog: true, credentialsId: '04c4fe5a-c72f-4e4f-8d7d-86fb3e798317')
		}
		
	
	}
	
	stage('Build'){
		steps{
			bat '''
			
			mvn clean install
		'''
		}
	
	}
	
	stage('Sonarqube') {
		environment {
        scannerHome = tool 'SonarQubeScanner1'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
            bat "${scannerHome}/bin/sonar-scanner"
			
        }
		script{
			def qualitygate = waitForQualityGate()
			
			if (qualitygate.status != "OK") {
				error "Pipeline aborted due to quality gate coverage failure: ${qualitygate.status}"
				
		}
        
      }
    }
	
	}
	
	stage('Upload Jar'){
		steps{
			bat '''
			echo "success"
		'''
		}
	
	}
	
	
	
	
	
}

}
