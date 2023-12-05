pipeline {
      agent { label 'jenkinsslave || jenkinsslave2'}
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
		stage('Example Test') {
            steps {
                echo 'creating war artifact'
                sh 'mvn clean package'
			}
		}
    }
}


