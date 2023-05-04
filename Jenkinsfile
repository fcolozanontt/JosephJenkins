pipeline {

    agent any
    stages {

        stage('Checkout Codebase'){
            steps{
                cleanWs()
                checkout scm: [$class: 'GitSCM', branches: [[name: '*/main']],userRemoteConfigs:
                [[url: 'https://github.com/fcolozanontt/JosephJenkins.git']]]
                bat 'dir'
            }
        }

        stage('Build'){
            steps{
                echo 'Checkpoint 1'
                bat 'cd src & javac -cp "lib\\junit-platform-console-standalone-1.7.0-all.jar" "src\\Car.java"'
                echo 'Checkpoint 2'
                bat 'cd src & javac -cp "..\\lib\\junit-platform-console-standalone-1.7.0-all.jar" CarTest.java'
                echo 'Checkpoint 3'
                bat 'cd src & javac -cp "..\\lib\\junit-platform-console-standalone-1.7.0-all.jar" App.java'
                echo 'Checkpoint 4'
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