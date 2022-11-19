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
            mail bcc: '', body: 'Jenkins is unable to code from git repository', cc: '', from: '', replyTo: '', subject: 'Download failed', to: 'gitadmin@gmail.com'
            exit(1)
        }
    }
    
    stage('Continuous Build') 
    {
        try
        {
        sh 'mvn package'
        }
        catch (Exception e2)
        {
            mail bcc: '', body: 'Jenkins is unable to build the code', cc: '', from: '', replyTo: '', subject: 'Build failed', to: 'dev@gmail.com'
            exit(1)
        }
    }
    stage('Continuous Deploy') 
    {
        deploy adapters: [tomcat9(credentialsId: 'c755d822-93a6-499b-9a8c-875b2afb3aae', path: '', url: 'http://172.31.42.1:8080')], contextPath: 'test', war: '**/*.war'
    }
     stage('Continuous testing') 
    {
        git 'https://github.com/OmkarAnk/Functional_testing.git'
        sh 'java -jar /home/ubuntu/.jenkins/workspace/test/testing.jar'
    }
    stage('Continuous delivery') 
    {
       deploy adapters: [tomcat9(credentialsId: 'c755d822-93a6-499b-9a8c-875b2afb3aae', path: '', url: 'http://172.31.42.143:8080')], contextPath: 'prod', war: '**/*.war'
    }
    
    
}
