pipeline{
    agent any

    stages{
        stage('Checkout'){
            steps{
                git branch: 'main', url:'https://github.com/ziyameng/lbg-vat-calculator.git'
            }
        }

        stage('SonarQube Analysis'){
            environment{
                scannerHome = tool 'sonarqube'
            }
            steps{
                WithSonarQubeEnv('sonar-qube-1'){
                    sh"${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
