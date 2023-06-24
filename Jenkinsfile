pipeline{
    agent any 
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }
    environment{
        SNAP_REPO = 'maven-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin'
        RELEASE_REPO = 'maven-release'
        CENTRAL_REPO = 'maven-central-repo'
        NEXUSIP = '172.31.20.149'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }
    stages {
        stage('Build with maven'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    echo "Now Archiving....."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Checkstyle Analysis'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
    }
}