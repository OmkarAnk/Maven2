node('built-in') 
{
    stage('Continuous download') 
    {
        try
        {
            git 'https://github.com/OmkarAnk/maven.git'
        }   
        catch (Exception e1)
        {
            mail bcc: '', body: 'Jenkins is unable to download the code', cc: '', from: '', replyTo: '', subject: 'Continuous download failed', to: 'gitadmin@gmail.com'
            exit(1)
        }
    }
    stage('Continuous build') 
    {
        try
        {
            sh 'mvn package'
        }   
        catch (Exception e2)
        {
            mail bcc: '', body: 'Jenkins is unable to build the code', cc: '', from: '', replyTo: '', subject: 'Continuous download failed', to: 'gitadmin@gmail.com'
            exit(1)
        }
    }
    stage('Continuous deploy') 
    {
        try
        {
            deploy adapters: [tomcat9(credentialsId: 'bed67ebe-4439-4af0-8718-5f01b09abdda', path: '', url: 'http://172.31.35.127:8080')], contextPath: 'test', war: '**/*.war'
        }   
        catch (Exception e3)
        {
            mail bcc: '', body: 'Jenkins is deploy to the artifact', cc: '', from: '', replyTo: '', subject: 'Continuous deployment failed', to: 'gitadmin@gmail.com'
            exit(1)
        }
    }
    stage('Continuous test') 
    {
        try
        {
          git 'https://github.com/OmkarAnk/Functional_testing.git'
          sh 'java -jar /home/ubuntu/.jenkins/workspace/demo/testing.jar'
        }   
        catch (Exception e4)
        {
            mail bcc: '', body: 'testing failed', cc: '', from: '', replyTo: '', subject: 'Continuous testing failed', to: 'gitadmin@gmail.com'
            exit(1)
        }
    }
    stage('Continuous delivery') 
    {
        try
        {
          deploy adapters: [tomcat9(credentialsId: 'bed67ebe-4439-4af0-8718-5f01b09abdda', path: '', url: 'http://172.31.45.26:8080')], contextPath: 'prod', war: '**/*.war'
        }   
        catch (Exception e5)
        {
            mail bcc: '', body: 'continuous delivery failed', cc: '', from: '', replyTo: '', subject: 'Continuous testing failed', to: 'gitadmin@gmail.com'
            exit(1)
        }
    }
}
