pipeline {
    agent any
    tools {
        maven "Maven3"
        jdk "OracleJDK8"
    }
    
    environment {
        SNAP_REPO = 'maven-snapshot'
		NEXUS_USER = 'rahul'
		NEXUS_PASS = '1234'
		RELEASE_REPO = 'maven-releases'
		CENTRAL_REPO = 'maven-central'
		NEXUSIP = '172.31.27.163'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'maven-public'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -U -s settings.xml -DskipTests install'
            }
        }
    }
}
