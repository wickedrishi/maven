node('master')
{
    stage('ContinuousDownload') 
    {
        git 'https://github.com/wickedrishi/maven.git'
    }
    stage('ContinuousBuild') 
    {
        sh label: '', script: 'mvn package'
    }
    stage('ContinuousDeployment')
    {
        sh label: '', script: '''scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.25.74:/var/lib/tomcat9/webapps/newtestapp.war
'''
    }
    stage('ContinuousTesting') 
    {
        git 'https://github.com/wickedrishi/FunctionalTesting.git'
        sh label: '', script: '''java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline/testing.jar
'''
    }
    stage('ContinuousDelivery')
    {
        input message: 'Waiting for approval from DM', submitter: 'srinivas'
        sh label: '', script: '''scp /home/ubuntu/.jenkins/workspace/ScriptedPipeline/webapp/target/webapp.war ubuntu@172.31.27.44:/var/lib/tomcat9/webapps/newprodapp.war
'''
    }
}
