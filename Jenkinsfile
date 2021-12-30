pipeline {
    agent any
    
    environment {
        
        dotnet='C:\\Program Files (x86)\\dotnet'
        awscli = "C:\\Program Files\\Amazon\\AWSCLIV2\\awscli"
        workspace = 'C:\\Program Files (x86)\\Jenkins'
    }

    stages {
        stage("Env Build Number"){
            steps{
                echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}"                                                
            }
        }
        stage('Checkout') {
            steps {
             git 'https://github.com/Tanukusolman/msbuild_project.git' 
                echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}"                                               
            }
        }
        stage('Restore') {
            steps {
                bat 'dotnet restore C:\Program Files (x86)\Jenkins'
                echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
            }
            
        }
        stage('Clean') {
            steps {
                bat 'dotnet clean C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
            }
        }
        stage('Build') {
            steps {
                bat 'dotnet build C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'           
            echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
            }
        }
        stage('Unit Test') {
            steps {
                bat 'dotnet test C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
            }
        }
        stage('Publish') {
            steps {
                bat 'dotnet publish C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
            }
        }
       stage ('Versioning') {
        steps {
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '0a607455-6969-4f96-af53-5a23eedf1ae0', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
{
bat'aws s3api put-bucket-versioning --bucket BuildBucket --versioning-configuration Status=Enabled'

}
}
}
        stage('Uploading') {
               steps {
      // you need cloudbees aws credentials
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '0a607455-6969-4f96-af53-5a23eedf1ae0', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                {
                    bat 'aws s3 ls'
                    bat 'aws s3 cp C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\buildpipeline\\ConsoleApp\\ConsoleApp\\bin\\Debug\\netcoreapp3.1\\ConsoleApp.dll  s3://buckerbuild1/BuildBucket//ConsoleApp.dll'
                echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
                }
            }
        }
    }
}
