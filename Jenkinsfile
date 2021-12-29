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
echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
}
}
}
 stage('list AppWebsites') {
steps {
bat 'C:\Windows\System32\inetsrv>appcmd list sites'
echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
}
}  
stage('restart AppWebsite') {
steps {
bat 'iisreset'
echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
}
}
 stage('stop AppWebsite') {
steps {
bat 'C:\\Windows\\System32\\inetsrv\\AppCmd stop site "default"'
echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
}
} 
stage('start AppWebsite') {
steps {
bat 'C:\\Windows\\System32\\inetsrv\\AppCmd start site "default"'
echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}" 
}
} 
}
}

