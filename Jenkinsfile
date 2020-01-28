pipeline{
    tools{
        jdk 'my_jdk'
        maven 'my_maven'
    }
    agent any
    stages{
        stage('checkout'){
            steps{
                git 'https://github.com/aungie/devopsclasscodes'
            }
        }
        stage('compile'){
            steps{
                sh 'mvn compile'
            }
        }
        stage('codereview'){
            steps{
                sh 'mvn pmd:pmd'
            }
            post {
                success {
                    pmd pattern: 'target/pmd.xml'
                }
            }
        }
        stage('unittest'){
            steps{
                sh 'mvn test'
            }
            post {
                success {
                    junit testResults: 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('metriccheck'){
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
            post {
                success {
                    cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                }
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
        }
    }
}
