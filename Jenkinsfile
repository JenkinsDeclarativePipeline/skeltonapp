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
                SONAR_CRED_VAR = '$SONAR_CRED_PSW'
            } 
            steps
            {
            echo "${SONAR_CRED_VAR}"
            withSonarQubeEnv('sonar-9.9.2') 
            {
        
            sh 'mvn clean sonar:sonar \
                -Dsonar.projectKey=maven-practice \
                -Dsonar.host.url=http://3.26.196.57:9000 \
                -Dsonar.login=${SONAR_CRED_VAR}'
        }
        }
    }
    
    }
}