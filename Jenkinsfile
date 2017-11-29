pipeline {
    agent any

    stages {
        
         stage('Displaying Parameters') {
            steps {
              echo 'Displaying parameter ${params.Test}'
            }
        }
        stage('Checking out from Github') {
            steps {
                git credentialsId: 'b408f6fb-227b-45ce-8d35-79b293ec3420', url: 'git@github.com:Sreenathplakkat1/HelloworldSample.git'
                echo 'Checkout from Github..'
            }
        }
        stage('Restore NugetPackages') {
            steps {
                bat 'C:\\Softwares/nuget.exe restore "C:\\Program Files (x86)\\Jenkins\\workspace\\DevopsLocal\\SampleApplication.sln"'
                echo 'Restoring Nuget packages..'
            }
        }
        stage('Build Solution') {
            steps {
                bat "\"${tool 'MSBuild'}\" SampleApplication.sln /p:Configuration=Debug /p:VisualStudioVersion=14.0"
                echo 'Build Solution..'
            }
        }
         stage('Test') {
            steps {
                echo 'Selenium testing....'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
