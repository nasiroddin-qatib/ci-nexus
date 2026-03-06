pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/nasiroddin-khatib/jenkins-sonarqube-ci'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }


	stage('Sonarqube') {
	    steps { 
	      withSonarQubeEnv('sonarqube') {
		sh 'mvn sonar:sonar'
	    }
	} 
}

	stage('Quality Gate') {
	    steps {
		waitForQualityGate abortPipeline: true
	    }
	}

        stage('Package') {
            steps {
                sh 'mvn clean package'
            }

        }


	stage('deploy') {
	    steps {
		sh 'mvn deploy'

		}
	}




    }
}

