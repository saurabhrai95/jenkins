pipeline{
agent any

environment {
    JAVA_HOME = 'C:\\Users\\saurabh_rai\\Desktop\\OpenJDK8U-x64_windows_8u212b04\\openjdk-8u212-b04'
	M2_HOME = 'C:\Users\saurabh_rai\Downloads\apache-maven-3.6.1-bin\apache-maven-3.6.1'
  }


stages{

	
	stage('Checkout') {
		steps{
			bat '''
			echo "JAVA_HOME = ${env.JAVA_HOME}"
			echo "M2_HOME = ${env.M2_HOME}"
			echo "Checkout from git"
			git(url: 'https://github.com/saurabhrai95/read-service.git', branch: 'master', changelog: true, credentialsId: '04c4fe5a-c72f-4e4f-8d7d-86fb3e798317')
			'''
		}
	
	}
	
	stage('Build'){
		bat '''
			cd read-service
			${env.M2_HOME}/mvn install
		'''
	
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
