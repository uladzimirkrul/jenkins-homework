pipeline {
    agent any
    stages {
        stage ('deploy-on-push-master - Checkout') {
            checkout([$class: 'GitSCM', branches: [[name: 'refs/heads/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '35cccb33-e523-42b6-9c1d-d1aaa475ffbe', url: 'git@github.com:uladzimirkrul/jenkins-homework']]])
        }
        stage('Build') {
            steps {
                sh 'mvn -f pom.xml -B -DskipTests clean package'
            }
            post {
                success {
                    echo 'Success build'
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
