pipeline {
    agent any
parameters {
     string(name: 'MajorVersion', defaultValue: '1', description: 'MajorVersion')
     string(name: 'MinorVersion', defaultValue: '0', description: 'MinorVersion')
     string(name: 'PatchVersion', defaultValue: '0', description: 'PatchVersion')
     string(name: 'PrereleaseString', defaultValue: '0', description: 'PrereleaseString')
          
    }
    stages {
       
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
        stage('Change Assembly Version')
        {
            steps{
                powershell '''$path = "C:\\Program Files (x86)\\Jenkins\\workspace\\jenkins-pipeline-example2\\SampleApplication\\Properties\\AssemblyInfo.cs"
$pattern = \'\\[assembly: AssemblyVersion\\("(.*)"\\)\\]\'
(Get-Content $path) | ForEach-Object{
    if($_ -match $pattern){
        # We have found the matching line
        # Edit the version number and put back.
        $fileVersion = [version]$matches[1]
        $newVersion = "{0}.{1}.{2}.{3}" -f $env:MajorVersion,$env:MinorVersion,$env:BUILD_NUMBER,$env:PrereleaseString
        \'[assembly: AssemblyVersion("{0}")]\' -f $newVersion
    } else {
        # Output line as is
        $_
    }
} | Set-Content $path'''
                echo 'Changed assembly version '
            }
        }
        stage('Build Solution') {
            steps {
                bat "\"${tool 'MSBuild'}\" SampleApplication.sln /p:Configuration=Debug /p:VisualStudioVersion=14.0"
                echo 'Build Solution..'
            }
        }
        stage('Commit Assembly Version'){
            steps{
                git url: "ssh://git@github.com:Sreenathplakkat1/HelloworldSample.git",
                credentialsId: 'b408f6fb-227b-45ce-8d35-79b293ec3420'
                bat '''git commit -am "Merged assembly changes to master"
              git push '''
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
