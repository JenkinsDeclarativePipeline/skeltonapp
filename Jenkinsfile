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
            tools
            {
                maven 'mvn-3.9.5'
            }
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
                    sonar_cred = credentials('sonar-9.9.2')
                }
            steps
            {
                withSonarQubeEnv('sonar-9.9.2') 
                {
        
            sh "mvn sonar:sonar \
            -Dsonar.projectKey=maven-project \
            -Dsonar.host.url=http://3.26.196.57:9000 \
            -Dsonar.login=sqp_5a5a5ab5c37e4393ba8864f847d3e63bfa4f6be4"
        }
        }
    }
    }
}