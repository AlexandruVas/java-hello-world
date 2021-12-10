pipeline {
    agent any
    tools {
        maven 'Maven'
        jdk 'JDK11'
        jdk 'JDK8'
    }

    stages {
        stage('Clone source from Github') {
            steps {
                git branch: 'main',
                url: 'https://github.com/AlexandruVas/java-hello-world.git'
                checkout scm
                echo "Branch has been copied"  
            }
        }
        stage('Maven Build') {
            tools{
                jdk 'JDK8'
            }
            steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube') {
            tools{
                jdk 'JDK11'
            }
        environment {
            scannerHome = tool 'SonarQube Scanner'
        } 
        steps {
        withSonarQubeEnv(installationName: 'SonarQube') {
            sh 'mvn sonar:sonar -Dsonar.projectname=java-hello-world -Dsonar.host.url=http://172.17.0.3:9000 -Dsonar.login=1d8ac99a0c6c8bafa712dbc05b4dd2b9a0bcbc79'
            }   
        }

    }
}
}
