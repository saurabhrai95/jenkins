pipeline{
agent any
tools {
  maven 'apache-maven'
  jdk 'jdk1.8'
git 'git'
}
environment {
    JAVA_HOME = 'C:\\Users\\saurabh_rai\\Desktop\\OpenJDK8U-x64_windows_8u212b04\\openjdk-8u212-b04'
	M2_HOME = 'C:\\Users\\saurabh_rai\\Downloads\\apache-maven-3.6.1-bin\\apache-maven-3.6.1'
  }


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
