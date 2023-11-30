pipeline {
      agent any
	  tools{
	      maven 'apache-maven-3.9.4'
	  }

    stages {
        stage('code compilation') {
            steps {
                echo 'code compilation is in progress'
                sh 'mvn clean compile'
				echo 'code compilation is in done'

            }
        }
        stage('code QA execution') {
            steps {
                echo 'test case check in progress'
                sh 'mvn clean test'
            }
        }
        stage('Sonarqube') {
                environment {
                  scannerHome = tool 'qube'
               }
                   steps {
                        withSonarQubeEnv('sonar-server') {
                        sh "${scannerHome}/bin/sonar-scanner"
                        sh 'mvn sonar:sonar'
                    }
                        timeout(time: 10, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                    }
                }
        }
		stage('Example Test') {
            steps {
                echo 'creating war artifact'
                sh 'mvn clean package'
			}
		}
    }
}