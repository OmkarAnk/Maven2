node('Built-in')
{
    stage('download')
    {
        try
        {
            git 'https://github.com/OmkarAnk/maven2.git'
        }
       catch(Exception e1)
       {
           mail bcc: '', body: 'jenkins is unable to download the code', cc: '', from: '', replyTo: '', subject: 'jenkisn is unable to download the code', to: 'git@admin'
           exit(1)
       }
       
    stage('build')
    {
        try
        {
            sh 'mvn clean package'
        }
        catch(Exception e2)
        {
            mail bcc: '', body: 'jenkins is unable to download the code', cc: '', from: '', replyTo: '', subject: 'jenkisn is unable to download the code', to: 'git@admin'
           exit(1)
        }
        stage('deploy')
        {
            scp /home/ubuntu/jenkins/workspace/practice0/webapp/target/webapp.war ubuntu@172.31.5.154:/etc/tomcat9/
        }
    }
    }
}
