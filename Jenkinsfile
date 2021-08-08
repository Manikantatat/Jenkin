pipeline
{
    agent any
    stages
    {
        stage('download')
        {
            steps 
            {
               script
               {
                   try
                   {
                       git 'https://github.com/intelliqittrainings/maven.git'
                   }
                   catch(Exception e1)
                   {
                     mail bcc: '', body: 'Jenkinfailed', cc: '', from: '', replyTo: '', subject: 'Jenkinfailed', to: 'mani@gmail.com'
                   }
               }
            }
        }
        stage('build')
        {
            steps 
            {
                sh 'mvn package '
            }
        }
        stage('deploy')
        {
            steps 
            {
                deploy adapters: [tomcat9(credentialsId: 'd8c9230a-495c-45a0-83e3-b0bf5a9eb8f0', path: '', url: 'http://172.31.11.60:8080')], contextPath: 'qaapp', war: '**/*.war'
            }
        }
        stage('testing')
        {
            steps 
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/declarativepipeline/testing.jar'
            }
        }
        
    }
    post
    {
        success
        {
            input message: 'Need approval', submitter: 'kesaram'
            deploy adapters: [tomcat9(credentialsId: 'd8c9230a-495c-45a0-83e3-b0bf5a9eb8f0', path: '', url: 'http://13.57.208.61:8080')], contextPath: 'paapp', war: '**/*.war'
        }
        failure
        {
           mail bcc: '', body: 'Jenkinfailed', cc: '', from: '', replyTo: '', subject: 'Jenkinfailed', to: 'mani@gmail.com' 
        }
    }
}
