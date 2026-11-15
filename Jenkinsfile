pipeline {
    agent any

    tools {
        maven 'M3'   // must match the name in Manage Jenkins > Tools
    }

    stages {
        stage('Build') {
            steps {
                dir('complete') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Test') {
            steps {
                dir('complete') {
                    sh 'mvn test'
                }
            }
        }

        stage('Push JAR to Nexus') {   // NEW
            steps {
                dir('complete') {
                    withCredentials([usernamePassword(credentialsId: 'nexus-creds',
                                                      usernameVariable: 'NEXUS_USER',
                                                      passwordVariable: 'NEXUS_PASS')]) {
                        sh 'mvn deploy -DskipTests -s settings.xml'
                    }
                }
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'complete/target/*.jar', fingerprint: true
        }
    }
}
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
