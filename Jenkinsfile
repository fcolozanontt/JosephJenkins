pipeline {

    agent any
    stages {

        stage('Checkout Codebase'){
            steps{
                cleanWs()
                checkout scm: [$class: 'GitSCM', branches: [[name: '*/main']],userRemoteConfigs:
                [[url: 'https://github.com/fcolozanontt/JosephJenkins.git']]]
                echo 'Printing dir from src'
                bat 'cd src'
                bat 'dir'
                bat 'cd ..'
                echo 'Printing dir from lib'
                bat 'cd lib'
                bat 'dir'
                bat 'cd ..'
            }
        }

        stage('Build'){
            steps{
                bat 'cd src'
                bat 'javac -cp "lib\\junit-platform-console-standalone-1.7.0-all.jar" CarTest.java Car.java App.java'
            }
        }

        stage('Test'){
            steps{
                bat 'cd src & java -jar ..\\lib\\junit-platform-console-standalone-1.7.0-all.jar -cp \".\" --select-class CarTest --reports-dir=\"reports\"'
                junit 'src/reports/*-jupiter.xml'
            }
        }

        stage('Deploy'){
            steps{
                bat 'cd src & java App' 
            }
        }
    }

}