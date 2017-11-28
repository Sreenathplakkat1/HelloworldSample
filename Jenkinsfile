pipeline {
    agent any

    stages {
        stage('Checking out from Github') {
            steps {
                git credentialsId: 'b408f6fb-227b-45ce-8d35-79b293ec3420', url: 'git@github.com:Sreenathplakkat1/HelloworldSample.git'
                echo 'Building..'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
