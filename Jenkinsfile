pipeline {
    agent {label 'agent' }
    tools { nodejs 'NodeJS'}

    environment {
        CI = 'true'
        registry = 'docker-services-training/aleesha/'
        }
    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Unit test') {
            steps {
                sh 'chmod +x ./jenkins/scripts/test.sh'
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Code Quality Check via SonarQube') {
   steps {
       script {
         def scannerHome = tool 'sonarqube';
           withSonarQubeEnv("sonarqube-container") {
           sh "${tool("sonarqube")}/bin/sonar-scanner \
           -Dsonar.projectKey=test-node-js \
           -Dsonar.sources=. \
           -Dsonar.css.node=. \
           -Dsonar.host.url=http://your-ip-here:9000 \
           -Dsonar.login=your-generated-token-from-sonarqube-container"
               }
           }
       }
   }
        // stage('SonarQube analysis') {
          //  steps {
            //    script {
              //      def scannerHome = tool 'sonarScan';
                //    withSonarQubeEnv('sonar') { // If you have configured more than one global server connection, you can specify its name
                  //      sh "${scannerHome}/bin/sonar-scanner"

                      }
                  }
             }
         }
        // stage('Artifactory') {
        //     steps {
        //         script {
        //             unstash name:"artifact"
        //             docker.withTool('docker') {
        //                 docker.withRegistry('https://artifactory.dagility.com', 'aleesha-registry'){
        //                     docker.build(registry + "nodejs:latest").push()
        //                 }
        //             }
        //         }
        //     }
        // }
    }
}
