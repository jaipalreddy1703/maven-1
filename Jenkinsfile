pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/jaipalreddy1703/maven-1.git'  
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeploy')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '1716cda0-83ea-4e76-9edd-3255575c47b4', path: '', url: 'http://172.31.1.234:8080')], contextPath: 'test', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
                
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '1716cda0-83ea-4e76-9edd-3255575c47b4', path: '', url: 'http://172.31.10.60:8080')], contextPath: 'prod', war: '**/*.war'
            }
        }
    }
}
