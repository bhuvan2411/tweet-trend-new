pipeline {
    agent {
        node {
            label 'maven'
        }
    }
 environment {
    PATH = "/opt/apache-maven-3.9.3/bin:$PATH"
 }
    stages {
        stage("build") {
            steps {
                echo "-------------------Build started-------------------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "-------------------Build completed-------------------"
            }
        }
        stage("test") {
            steps {
                echo "-------------------unit test started-------------------"
                sh 'mvn surefire-report:report'
                echo "-------------------unit test completed-------------------"
            }
        }
        stage('SonarQube analysis') {

            environment {
             scannerHome = tool 'bhuvan-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('bhuvan-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
      sh "${scannerHome}/bin/sonar-scanner"
      }
    
    }
  }
    }
}