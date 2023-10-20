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
        stage('SonarQube analysis')
            {
                environment
                {
                    sonar_cred = credentials('sonar-9.9.2')
                }
            steps
            {
                withSonarQubeEnv('sonar-9.9.2') 
                {
        
            sh 'mvn clean sonar:sonar \
            -Dsonar.projectKey=maven-project \
            -Dsonar.host.url=http://3.26.196.57:9000 \
            -Dsonar.login="$sonar_cred_PSW" '
        }
        }
    }
    stage('Build-Project')
        {
            
            steps
            {
                echo "===============================BUILD-PROJECT===================================="
                sh 'mvn package'
            }
        }
    }
}