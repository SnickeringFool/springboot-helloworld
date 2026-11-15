pipeline {
    agent any
    tools { maven 'M3' }
    stages {
        stage('Build') { 
		steps { 
			dir('complete') {
				sh 'mvn clean package -DskipTests' 
				}
	 		}
    		}
	}
}
