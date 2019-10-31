pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
	node('docker') {
 
    	    stage 'Build & UnitTest'
            	sh "docker build -t tomcat8:jenkins -f Dockerfile ."
  
	}


        stage('Deliver') {
            agent {
                docker { image 'tomcat8:jenkins' }
            } 

            steps {
                sh './scripts/deliver.sh'
            }
        }
    }
}
