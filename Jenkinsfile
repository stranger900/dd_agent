pipeline{
    agent any
    
    stages{
        stage('Git checkout'){
            steps{
                git 'https://github.com/stranger900/dd_agent.git'
            }
        }
        stage('deploy datadog agent for Kubernetes'){
            steps{
                withAWS(credentials: 'aws_credentials', region: 'us-east-1') {
                    // sh '/usr/local/bin/helm repo add datadog https://helm.datadoghq.com'
                    // sh '/usr/local/bin/helm repo add stable https://charts.helm.sh/stable'
                    // sh '/usr/local/bin/helm repo update'
                    sh '/usr/local/bin/helm install dd-agent -f values.yaml  --set datadog.apiKey=${DD_API_KEY} datadog/datadog --set targetSystem=linux'
                }
            }
        }
        stage('outputs'){
            steps{
                withAWS(credentials: 'aws_credentials', region: 'us-east-1') {
                    sh '/usr/local/bin/kubectl get pods'
                    sh '/usr/local/bin/kubectl get svc'
                }
            }
        }
    }
}