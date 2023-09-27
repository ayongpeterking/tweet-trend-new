pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}
    stages {
        stage("build") {
            steps {
                sh 'mvn clean deploy'
            }
        }
    }

    stage('SonarQube analysis') {
            environment {
            scannerHome = tool 'don-sonarqube-scanner'
            }
        steps { 
            echo '------------------- Sonar Started -------------'
        withSonarQubeEnv('don-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
            sh "${scannerHome}/bin/sonar-scanner"
    }
    echo '------------------- Sonar Analysis Completed -------------'
  }
}
    