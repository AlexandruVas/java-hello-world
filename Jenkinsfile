pipeline {
    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage('Clone source from Github') {
            steps {
                git branch: 'master',
                url: 'https://github.com/AlexandruVas/java-hello-world'
                checkout scm  
            }
        }
        stage('Maven Build') {
            tools{
                jdk 'JDK11'
            }
            steps {
                sh 'mvn install'
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
            sh 'mvn sonar:sonar ' +
                '-Dsonar.host.url=http://localhost:9000 ' +
                // '-Dsonar.sources=. ' +
                '-Dsonar.projectKey=project_test ' +
                '-Dsonar.login=2df3a596d45070ec4b31610f967b24c4ca9af2d8 ' +
                // '-Dsonar.java.binaries=. ' +
                // '-DskipTests=true' +
                // '-Dsonar.cfamily.build-wrapper-output=bw-output ' +
                '-Dsonar.projectName=project_test ' +
                '-Dsonar.projectVersion=$BUILD_NUMBER'
            }   
        }

    }
}
}
