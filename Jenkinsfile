pipeline {

    agent any
    parameters {
        string(name: 'param', defaultValue: 'value1', description: 'Descr') 
    }

    options {
        //OutputEnvironmentVariablesBuildWrapper('JAVA_HOME')
        wrap(delegate: [$class: 'com.microfocus.application.automation.tools.settings.OutputEnvironmentVariablesBuildWrapper', outputEnvironmentParameters: 'JAVA_HOME'])
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }
    stages {
        
        stage('Cleanup Workspace') {
            steps {                        
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """                              
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']]
                ])
            }
        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis"
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }

    }   
}
