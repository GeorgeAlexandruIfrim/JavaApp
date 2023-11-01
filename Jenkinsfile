pipeline {
    agent any
    // Add a tool configuration here...
    stages {
        stage('Source') {
            steps {
                git branch: 'master',
                    changelog: false,
                    poll: false,
                    url: 'https://github.com/GeorgeAlexandruIfrim/JavaApp.git'
            }
        }
        stage('Clean') {
            steps {
                dir("${env.WORKSPACE}/Ch05/05_04-challenge-create-artifacts-and-reports"){
                    echo "Cleaning the workspace..."
                    // Uncomment the following line after Maven is configured as a global tool
                     bat 'mvn clean'
                }
            }
        }
        stage('Test') {
            steps {
                dir("${env.WORKSPACE}/Ch05/05_04-challenge-create-artifacts-and-reports"){
                    echo "Running tests..."
                    // Uncomment the following line after Maven is configured as a global tool
                     bat 'mvn test'
                }
            }
        }

        stage('Clean and SonarQube Analysis') {
            // steps {
            //     // Use 'bat' to run Windows batch commands
            //     bat "\"${tool 'Maven'}/bin/mvn\" clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar"
            // }
            steps {
              withSonarQubeEnv('SonarQube') {
                bat 'mvn clean package sonar:sonar'
              }
            }
        }
    


        stage('Package') {
            steps {
                dir("${env.WORKSPACE}/Ch05/05_04-challenge-create-artifacts-and-reports"){
                    echo "Creating the JAR file..."
                    // Uncomment the following line after Maven is configured as a global tool
                     bat 'mvn package -DskipTests'
                }
            }
        }
    }
    post {
        always {
            echo "Collecting jUnit test results..."
            // Add jUnit report collection here...

            echo "Archiving the JAR file..."
            // Add artifact archiving here...
        }
    }
}
