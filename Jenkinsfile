@Library('jenkinssharedlibrary@master')_
 
pipeline{
    agent any
    stages{
        stage('Git Checkout'){
            steps{
                gitcheckout([
                    $class: 'GitSCM',
                    branch: "master",
                    url: 'https://github.com/BommanaJyothi/importedProject.git'
                ])
            }
        }
        stage('test'){
            steps{
                script{
                    test.call()        
                }
            }
        }
        stage('maven build'){
            steps{
                script{
                    build.compile()
                }
            }
        }
        stage('tomcat deploy'){
            steps{
                script{
                    deployWarfile([
                        adapters: [
                            tomcat7(credentialsId: 'tomcat', 
                            path: '', 
                            url: 'http://localhost:9090/')
                            ],
                        contextPath: "/MyWebapp",
                        war: "**/*.war"
                    ])
                }
            }
        }
        stage('jFrog artifactory'){
            steps{
                script {
                    artifactory([
                       server: 'jfrog',
                       tool: "maven"
                       ])
                }
            }
        }
    }
}
