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
    }
}

