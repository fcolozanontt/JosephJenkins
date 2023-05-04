pipeline {

    agent any
    stages {

        stage('Checkout Codebase'){
            steps{
                cleanWs()
            }
        }

        stage('Build'){
            steps{
                bat 'cd src'
                bat 'javac -cp "..\\lib\\junit-platform-console-standalone-1.7.0-all.jar" CarTest.java Car.java App.java'
                bat 'cd ..'
            }
        }

        stage('Test'){
            steps{
                bat 'cd src'
                bat 'java -jar ..\\lib\\junit-platform-console-standalone-1.7.0-all.jar -cp \".\" --select-class CarTest --reports-dir=\"reports\"'
                bat 'cd ..'
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