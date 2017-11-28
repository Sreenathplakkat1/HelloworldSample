pipeline {
    agent any

    stages {
         stage 'CheckOut code'
   git credentialsId: 'b408f6fb-227b-45ce-8d35-79b293ec3420', url: 'git@github.com:Sreenathplakkat1/HelloworldSample.git'
   stage 'Restore NugetPackages'
   bat 'C:\\Softwares/nuget.exe restore "C:\\Program Files (x86)\\Jenkins\\workspace\\DevopsLocal\\SampleApplication.sln"'
   stage 'Build Solution'
   bat "\"${tool 'MSBuild'}\" SampleApplication.sln /p:Configuration=Debug /p:VisualStudioVersion=14.0"
   stage 'Test'
   echo 'Testing Completed'
    }
}
