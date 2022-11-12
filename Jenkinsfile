pipeline
{
    agent any
    tools{
        maven "Maven3"
        jdk "OracleJDK8"
    }

    environment {
SNAP_REPO= 'vprofile-snapshot'
NEXUS_USER= 'admin'
NEXUS_PASS='1234'
RELEASE_REPO='vprofile-release'
CENTRAL_REPO='vpro-maven-central'
NEXUSIP='172.31.19.81'
NEXUSPORT='8081'
NEXUS_GRP_REPO='vpro-maven-group'
NEXUS_LOGIN='nexuslogin'
SONARSERVER='sonarserver'
SOANRSCANNER='sonarscanner'
}
 
    stages{
        stage('Build'){
            steps{
            sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    echo "now archiving"
                    archiveArtifacts artifacts:'**/*.war'
                        }
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('checkstyle Analysis'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
          stage('Sonar Analysis') {
            environment {
                scannerHome = tool "${SONARSCANNER}"
            }
            steps {
               withSonarQubeEnv("${SONARSERVER}") {
                   sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
              }
            }
          }
    }
}