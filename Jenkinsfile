pipeline {
    agent any

    environment {
        ENV = 'dev'          // Set default environment
        APP_NAME = 'MyApp'
    }

    options {
        skipDefaultCheckout() // We'll checkout manually from GitHub
    }

    stages {

        stage('Checkout from GitHub') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/LakshmiVanchireddy/LakshmiVanchireddy/blob/main/Jenkinsfile'  // 🔁 Replace with your repo
                    ]]
                ])
            }
        }

        stage('Build') {
            when {
                expression { env.ENV }
            }
            steps {
                echo "Environment: ${ENV}"
                echo "Building ${APP_NAME}..."
                // Example: sh 'mvn clean install'
            }
        }

        stage('Test') {
            when {
                expression { env.ENV }
            }
            steps {
                echo "Running tests for ${APP_NAME}..."
                // Example: sh 'mvn test'
            }
        }

        stage('Deploy') {
            when {
                expression { env.ENV }
            }
            steps {
                echo "Deploying ${APP_NAME} to environment: ${ENV}"
                // Example: sh './deploy.sh'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline executed successfully!'
            // You can add notifications here (Slack, email, etc.)
        }
        failure {
            echo '❌ Pipeline failed.'
            // You can add alerting logic here too
        }
        always {
            echo '📌 Pipeline execution completed.'
        }
    }
}
