pipeline{
agent any
tools{
	maven 'apache-maven'
	jdk 'jdk1.8'
}

}
stages{

	stage('Initialization') {
		steps {
			bat '''
				
			echo "JAVA_HOME = ${JAVA_HOME}"
			echo "M2_HOME = ${M2_HOME}"
			'''
		}
	
	}
	stage('Checkout') {
		steps{
			bat '''
			echo "Checkout from git"
			'''
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