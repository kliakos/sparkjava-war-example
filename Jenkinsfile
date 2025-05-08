pipeline{
    agent any
    environment{
        PATH="/opt/maven/bin:$PATH"
    }
    stages{
        stage('git clone'){
            steps{
            git url: "https://github.com/Mariselvam5/sparkjava-war-example.git", branch: "master"
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean install'
            }
        }
    }
