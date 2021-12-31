pipeline {
agent any

environment {

awscli = "C:\\Program Files\\Amazon\\AWSCLI\\bin"
appcmd = "C:\\Windows\\System32\\inetsrv"
}
stages {
stage('S3download') {
steps {
withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '0a607455-6969-4f96-af53-5a23eedf1ae0', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
{
bat 'aws s3 cp s3://buckerbuild1/BuildBucket//ConsoleApp.dll D:\\Artifact'
echo "The build number is ${env.TAG_TIMESTAMP}"
                echo "You can also use \${TAG_TIMESTAMP} -> ${TAG_TIMESTAMP}" 
}
}
}
   stage('Unzip') {
         steps  {
                bat 'C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell Expand C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\build_pipeline\\ConsoleApp\\ConsoleApp\\bin\\Release\\netcoreapp3.1\\ConsoleApp.dll.zip C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\build_pipeline\\ConsoleApp\\ConsoleApp\\bin\\Release\\netcoreapp3.1\\ConsoleApp.dll '
                echo "END - ZIP"
            }
        }
 stage('list AppWebsites') {
steps {
bat 'C:\\Windows\\System32\\inetsrv\\appcmd list sites'
echo "The build number is ${env.GIT_LOCAL_BRANCH}"
                echo "You can also use \${GIT_LOCAL_BRANCH} -> ${GIT_LOCAL_BRANCH}"  
}
}  
stage('restart AppWebsite') {
steps {
bat 'iisreset'
echo "The build number is ${env.EXECUTOR_NUMBER}"
                echo "You can also use \${EXECUTOR_NUMBER} -> ${EXECUTOR_NUMBER}"  
}
}
 stage('stop AppWebsite') {
steps {
bat 'C:\\Windows\\System32\\inetsrv\\AppCmd stop site "default"'
echo "The build number is ${env.BUILD_TAG}"
                echo "You can also use \${BUILD_TAG} -> ${BUILD_TAG}"  
}
} 
stage('start AppWebsite') {
steps {
bat 'C:\\Windows\\System32\\inetsrv\\AppCmd start site "default"'
echo "The build number is ${env.JENKINS_URL}"
                echo "You can also use \${JENKINS_URL} -> ${JENKINS_URL}"  
}
} 
}
}

