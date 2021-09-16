pipeline {
    agent any
     triggers {
        githubPush()
      }
    stages {
        stage('Restore packages'){
           steps{
               sh 'dotnet restore WebApplication.sln'
            }
         }        
        stage('Clean'){
           steps{
               sh 'dotnet clean WebApplication.sln --configuration Release'
            }
         }
        stage('Build'){
           steps{
               sh 'dotnet build WebApplication.sln --configuration Release --no-restore'
            }
         }
        stage('Publish'){
           steps{
               sh 'dotnet publish WebApplication/WebApplication.csproj --configuration Release --no-restore'
             }
        }
        stage('Push') {
            steps {
              sh """
              cd ${WORKSPACE}/WebApplication/bin/Release
              /bin/zip -r netcoreapp3_1.zip netcoreapp3.1/
              /bin/jfrog rt u netcoreapp3_1.zip  dotnetcore/   --url http://34.141.137.211:8082/artifactory --user admin --password Emids9211!
               """
}
}
     
    }
}
