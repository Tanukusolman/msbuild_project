pipeline {
    agent any
    
    environment {
        
        dotnet='C:\\Program Files (x86)\\dotnet'
        awscli = "C:\\Program Files\\Amazon\\AWSCLIV2\\awscli"
    }

    stages {
        stage('Checkout') {
            steps {
             git 'https://github.com/Tanukusolman/msbuild_project.git'   
            }
        }
        stage('Restore') {
            steps {
                bat 'dotnet restore C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            }
        }
        stage('Clean') {
            steps {
                bat 'dotnet clean C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            }
        }
        stage('Build') {
            steps {
                bat 'dotnet build C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'           
            }
        }
        stage('Unit Test') {
            steps {
                bat 'dotnet test C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            }
        }
        stage('Publish') {
            steps {
                bat 'dotnet publish C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            }
        }
       
        stage('Uploading') {
               steps {
      // you need cloudbees aws credentials
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '0a607455-6969-4f96-af53-5a23eedf1ae0', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                {
                    bat 'aws s3 ls'
                    bat 'aws s3 cp C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\bin\\Debug\\netcoreapp3.1\\ConsoleApp.dll  s3://buckerbuild1/BuildBucket//ConsoleApp.dll'
                }
            }
        }
    }
}
