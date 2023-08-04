pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
               sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: 'f2495eb1-0bfb-43bd-85c4-52e9309ce41a', path: '', url: 'http://172.31.86.147:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
         stage('ContTesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar  /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
         stage('ContDelivery')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: 'f2495eb1-0bfb-43bd-85c4-52e9309ce41a', path: '', url: 'http://172.31.81.197:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
    }
}
