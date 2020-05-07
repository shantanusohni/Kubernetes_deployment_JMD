pipeline {
    agent any
    stages {
        stage('Deploy Staging') {
            steps{
                git url: 'https://github.com/shantanusohni/Kubernetes_deployment_JMD.git'
                step([$class: 'KubernetesEngineBuilder', 
                        projectId: "fresh-shell-275710",
                        clusterName: "jaimatadi",
                        zone: "us-central1-a",
                        manifestPattern: 'deployment.yaml',
                        credentialsId: "gke",
                        verifyDeployments: true])
            }
        }
        stage('Wait for SRE Approval') {
         steps{
           timeout(time:12, unit:'HOURS') {
              input message:'Approve deployment?', submitter: 'sre-approvers'
           }
         }
        }
        stage('Deploy Production') {
            steps{
                git url: 'https://github.com/shantanusohni/Kubernetes_deployment_JMD.git'
                step([$class: 'KubernetesEngineBuilder', 
                        projectId: "fresh-shell-275710",
                        clusterName: "jaimatadi",
                        zone: "us-central1-a",
                        manifestPattern: 'deployment.yaml',
                        credentialsId: "gke",
                        verifyDeployments: true])
            }
        }
    }
}