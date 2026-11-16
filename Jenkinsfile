
pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Java Project'

                script {
                    if (isUnix()) {
                        sh 'mvn clean compile'
                    } else {
                        bat 'mvn clean compile'
                    }
                }
            }
        }

        stage('Unit Test') {
            steps {
                echo 'Running JUnit Tests'

                script {
                    if (isUnix()) {
                        sh 'mvn test'
                    } else {
                        bat 'mvn test'
                    }
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging Java Project'

                script {
                    if (isUnix()) {
                        sh 'mvn package -DskipTests'
                    } else {
                        bat 'mvn package -DskipTests'
                    }
                }
            }
        }

        stage('Publish JUnit Report') {
            steps {
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }

    post {
        always {
            echo 'Jenkins Pipeline Execution Completed'
            junit allowEmptyResults: true,
                  testResults: '**/target/surefire-reports/*.xml'
        }

        success {
            echo 'Build Successful!'
        }

        failure {
            echo 'Build Failed!'
        }
    }
}
