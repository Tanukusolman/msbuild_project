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
}
}
}
 stage('list AppWebsite') {
steps {
bat 'list sites'
}
} 
stage('start AppWebsite') {
steps {
bat 'start site "default"'
}
}  
  
stage('restart AppWebsite') {
steps {
bat 'iisreset'
}
}
}
}

