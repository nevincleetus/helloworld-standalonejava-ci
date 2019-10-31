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
	stage('Building image') {
        	steps{
        	    script {
                        docker.build tomcat8:jenkins
                    }
               }
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
