    pipeline {
    agent {
        node {
            label 'Jenkins_Agent'}
    }
        tools {
        maven 'Maven3' // Name configured in Global Tool Configuration
        jdk 'Java17'
}

        stages {
            stage('Cleanup WorkSpace') {
                steps {
                    cleanWs()
                }
            }
            stage('Checkout From SCM') {
                steps { // Same with GitPull
                    git branch : 'main', credentialsId : 'Github' , url : 'https://github.com/NHKyaw/Devops_Lab_register-app.git'
                }
            }

            stage('Build Application') {
                steps {
                    sh 'mvn clean package'
                }
            }

            stage('Test Application') {
                steps {
                    sh 'mvn test'
                }
            }

            stage('SonarQube Analysis') {
                steps {
                    script {
                        withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token', installationName: 'jenkins-sonarqube-token') {
                            sh "mvn sonar:sonar"
                        }
                    }
                }
            }

                        stage('SonarQube Quality Gate') {
                steps {
                    script {
                        waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonarqube-token'
                    }
                }
            }
    }
}

