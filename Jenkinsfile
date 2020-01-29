pipeline {
    tools {
        jdk 'my_jdk'
        maven 'my_maven'
    }
    agent {
        label 'windows'
    }
    stages {
        stage('checkout') {
            steps{
                git 'https://github.com/aungie/devopsclasscodes'
            }
        }
        stage('compile') {
            steps {
                bat 'mvn compile'
            }
        }
        stage('codereview') {
            steps{
                bat 'mvn pmd:pmd'
            }
            post {
                success {
                    pmd pattern: 'target/pmd.xml'
                }
            }
        }
        stage('unittest') {
            steps {
                bat 'mvn test'
            }
            post {
                success {
                    junit testResults: 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('metriccheck') {
            steps {
                bat 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
            post {
                success {
                    cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                }
            }
        }
        stage('package') {
            steps {
                bat 'mvn package'
            }
        }
    }
}
