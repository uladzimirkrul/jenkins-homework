pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                        credentialsId: 'jenkins-ssh',
                        url: 'ssh://git@github.com:uladzimirkrul/jenkins-homework.git'
                sh "ls -lat"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -f pom.xml -B -DskipTests clean package'
            }
            post {
                success {
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -f pom.xml test'
            }
            post {
                always {
                    junit '/target/surefire-reports/*.xml'
                }
            }
        }
    }
}
