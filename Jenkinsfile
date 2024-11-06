pipeline{
    agent any
    environment{
        DOCKER_LOGIN=credentials('DOCKER_LOGIN')
    }

    stages{
        stage('Docker Login'){
            steps{
                sh 'docker login -u ${DOCKER_LOGIN_USR} -p ${DOCKER_LOGIN_PSW}'
            }
        }
        stage('Checkout'){
            steps{
                git branch: 'main', url:'https://github.com/ziyameng/lbg-vat-calculator.git'
            }
        }
        stage('Install'){
            steps{
                sh "npm install"
            }
        }
        stage('Test'){
            steps{
                sh "npm test"
            }
        }
        stage('SonarQube Analysis'){
            environment{
                scannerHome = tool 'sonarqube'
            }
            steps{
                withSonarQubeEnv('sonar-qube-1'){
                    sh"${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
