pipeline {
    agent any
    tools {
        maven 'NewMaven'   // name from Jenkins tool configuration
    }
    stages {
        stage('Clone Repo') {
            steps {
                echo "Cloning repo..."
                git url: "https://github.com/SaikeerthanaElagam/DevopsPipeline.git", branch: 'master'
            }
        }
        stage('Build') {
            steps {
                echo "Cleaning and building the project..."
                bat "mvn clean compile"
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
                bat "mvn test"
            }
        }
        stage('Deploy and Package') {
            steps {
                echo "Packaging application as JAR/WAR/EAR..."
                bat "mvn package"
            }
        }
        stage('Archive Artifacts') {
            steps {
                echo "Archiving artifacts..."
                archiveArtifacts artifacts: 'target/*.jar, target/*.war, target/*.ear', fingerprint: true
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
