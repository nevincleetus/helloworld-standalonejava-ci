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

	stage('Build Image') {
            steps {
                script {
                    sh 'docker build -t tomcat8:jenkins .'
                }
            }
        }
	//stage('Building image') {

          // agent {
           // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
           //    dockerfile {
           //       filename 'Dockerfile.build'
           //       label 'tomcat8:jenkins'
           //       args '-v /tmp:/tmp'
           //    }
           // }

        //}

        stage('Deliver') {

            steps {
                sh './scripts/deliver.sh'
            }
        }
    }
}
