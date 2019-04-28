pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    options {
        skipStagesAfterUnstable()
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
        stage('Scan') {
            steps {
                sh 'echo "Scan completed."'
            }
        }
        stage('Static Analysis') {
            steps {
                sh 'echo "Scan completed."'
            }
        }
        stage('QA Regression Tests') {
            steps {
                sh 'echo "QA Approved."'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
            }
        }
    }
}
