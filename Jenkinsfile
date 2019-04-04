pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
				// OK
                sh 'mvn -B -DskipTests clean package'
				nexusPolicyEvaluation failBuildOnNetworkError: false, iqApplication: selectedApplication('sandbox-application'), iqStage: 'build', jobCredentialsId: '9880fe95-7307-4700-8879-f836ea34bce0'
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
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
