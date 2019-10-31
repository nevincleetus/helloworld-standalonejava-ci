pipeline {
    agent none  
    stages {
        stage('Build') {
           agent {
               docker {
                  image 'maven:3-alpine'
                  args '-v /root/.m2:/root/.m2'
               }
            }
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            agent {
               docker {
                  image 'maven:3-alpine'
                  args '-v /root/.m2:/root/.m2'
               }
            }
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

           agent {
           // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
               dockerfile {
                  filename 'Dockerfile.build'
                  label 'tomcat8:jenkins'
                  args '-v /tmp:/tmp'
               }
            }

            steps{
                 script {
                    docker.build("tomcat8:jenkins")
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
