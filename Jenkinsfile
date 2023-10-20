pipeline
{
    agent
    {
        label 'maven'
    }
    parameters
    {
        string(name: 'branch', defaultValue: 'master', description: 'Enter branch name')
    }
    tools
            {
                maven 'mvn-3.9.5'
            }       
    stages
    {
        stage('SCM-Checkout')
        {
            steps
            {
                echo "===============================${branch}===================================="
                checkout scmGit(branches: [[name: '${branch}']],
                userRemoteConfigs: [
                    [ url: 'https://github.com/JenkinsDeclarativePipeline/skeltonapp.git' ]
                ])
            }
        }
        stage('Build-Project')
        {
            
            steps
            {
                echo "===============================BUILD-PROJECT===================================="
                sh 'mvn clean package'
            }
        }
        stage('SonarQube analysis')
            {
            environment
            {
                SONAR_CRED = credentials('sonar-9.9.2')
                //SONAR_CRED_VAR = '$SONAR_CRED_PSW'
            } 
            steps
            {
                echo 'sonar-cred $SONAR_CRED_PSW'
            }
    }
    
    }
}