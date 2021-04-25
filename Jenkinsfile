pipeline {
    agent {
        docker {
            image 'maven:3.3.3'
            args '-v C:\\Users\\kdjlyy\\.m2:/root/.m2'
        }
    }
    stages {
        stage('Compile') {
            steps {
                sh 'mvn -B clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Site') {
            steps {
                sh 'mvn site'
            }
            post {
                always {
                    cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
                    publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/site', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: 'site report'])
                }
            }
        }
        stage('Deliver') {
            steps {
                sh("echo lj1837520|su -s ./jenkins/scripts/deliver.sh")
                //sh 'echo lj1837520|sudo -S ./jenkins/scripts/deliver.sh'
            }
        }
    }
}