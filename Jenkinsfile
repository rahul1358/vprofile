pipeline {
    agent any
    tools {
        maven "Maven3"
        jdk "OracleJDK8"
    }
    
    environment {
        SNAP_REPO = 'vprofile_snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = '1234'
		RELEASE_REPO = 'vprofile_release'
		CENTRAL_REPO = 'vprofile_maven_central'
		NEXUSIP = '172.31.27.163'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vprofile_maven_group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
        }
    }
}
