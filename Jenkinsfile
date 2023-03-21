node('built-in') 
{
    stage('Continuous download')
    {
        try
        {
            git 'https://github.com/OmkarAnk/maven.git'
        }
        catch(Exception e1)
        {
            mail bcc: '', body: 'Jenkins is unable to download the code from git repository.', cc: '', from: '', replyTo: '', subject: 'Continuous download failed', to: 'gitadmin@gmail.com'
            exit(1)
        }
    }
    stage('Continuous build')
    {
        try
        {
            sh 'mvn package'
        }
        catch(Exception e2)
        {
            mail bcc: '', body: 'Jenkins is unable to build the code.', cc: '', from: '', replyTo: '', subject: 'Continuous build failed', to: 'devteam@gmail.com'
            exit(1)
        }
    }
    stage('Continuous deploy')
    {
        try
        {
            deploy adapters: [tomcat9(credentialsId: '5fc8d8ff-eecc-4a9a-b5c4-8ec30db32dd0', path: '', url: 'http://172.31.5.154:8080')], contextPath: 'test', war: '**/*.war'
        }
        catch(Exception e3)
        {
            mail bcc: '', body: 'Jenkins is unable to deploy the code on qa server.', cc: '', from: '', replyTo: '', subject: 'Continuous build failed', to: 'middlewareteam@gmail.com'
            exit(1)
        }
    }
    stage('Continuous testing')
    {
        try
        {
            git 'https://github.com/OmkarAnk/Functional_testing.git'
            sh 'java -jar /home/ubuntu/.jenkins/workspace/trail1/testing.jar'
        }
        catch(Exception e4)
        {
            mail bcc: '', body: 'Jenkins is unable to test the code on qa server.', cc: '', from: '', replyTo: '', subject: 'Continuous build failed', to: 'qaeam@gmail.com'
            exit(1)
        }
    }
    stage('Continuous delivery')
    {
        try
        {
            deploy adapters: [tomcat9(credentialsId: '5fc8d8ff-eecc-4a9a-b5c4-8ec30db32dd0', path: '', url: 'http://172.31.10.75:8080')], contextPath: 'prod', war: '**/*.war'
        }
        catch(Exception e5)
        {
            mail bcc: '', body: 'Jenkins is unable to deliver the code on prod server.', cc: '', from: '', replyTo: '', subject: 'Continuous delivery failed', to: 'delivery@gmail.com'
            exit(1)
        }
    }
     
}
