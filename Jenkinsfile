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
                bat 'dir'
                
                bat 'mkdir lib'
                
                bat 'cd lib'
                bat 'powershell -Command "(New-Object System.Net.WebClient).DownloadFile('https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.7.0/junit-platform-console-standalone-1.7.0-all.jar', 'junit-platform-console-standalone-1.7.0-all.jar')"'
                bat 'cd ..'

                bat 'cd src'
                bat 'javac -cp "..\lib\junit-platform-console-standalone-1.7.0-all.jar" CarTest.java Car.java App.java'
                bat 'cd ..'
            }
        }

        stage('Test'){
            steps{
                bat 'cd src/ ; java -jar ../lib/junit-platform-console-standalone-1.7.0-all.jar -cp "." --select-class CarTest --reports-dir="reports"'
                junit 'src/reports/*-jupiter.xml'
            }
        }

        stage('Deploy'){
            steps{
                sh 'cd src/ ; java App' 
            }
        }
    }

}