pipeline {

    agent any
    environment {
        LOG_JUNIT_RESULTS='true'
    }
    stages {

        stage('Checkout Codebase'){
            steps{
                cleanWs()
                checkout scm: [$class: 'GitSCM', branches: [[name: '*/main']],userRemoteConfigs:
                [[url: 'https://github.com/fcolozanontt/JosephJenkins.git']]]
            }
        }

        stage('Build'){
            steps{
                bat 'cd src & javac -cp "..\\lib\\junit-platform-console-standalone-1.7.0-all.jar" CarTest.java Car.java App.java'
            }
        }

        stage('Test'){
            steps{
                bat 'cd src & java -jar ..\\lib\\junit-platform-console-standalone-1.7.0-all.jar -cp \".\" --select-class CarTest --reports-dir=\"reports\"'
                junit 'src/reports/*-jupiter.xml'
                influxDbPublisher(selectedTarget: 'junit-test-data')
            }
        }

        stage('Deploy'){
            steps{
                bat 'cd src & java App' 
            }
        }
    }

}