pipeline{
agent any

tools {
  maven 'apache-maven'
  jdk 'jdk1.8'
}

environment {
    JAVA_HOME = 'C:\\Users\\saurabh_rai\\Desktop\\OpenJDK8U-x64_windows_8u212b04\\openjdk-8u212-b04'
	M2_HOME = 'C:\\Users\\saurabh_rai\\Downloads\\apache-maven-3.6.1-bin\\apache-maven-3.6.1'
  }


stages{

	
	stage('Checkout') {
		steps{
			git(url: 'https://github.com/saurabhrai95/read-service.git', branch: 'master', changelog: true, credentialsId: '04c4fe5a-c72f-4e4f-8d7d-86fb3e798317')
		}
		
	
	}
	
	stage('Unit Test'){
		steps{
			bat '''
			cd read-service
			mvn test
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
	
	stage('Build'){
		steps{
			bat '''
			cd read-service
			mvn install
		'''
		}
	
	}
	
	
	
	
	
}

}
