pipeline {
    agent any

    environment {
        // Define the recipient for email notifications
        EMAIL_RECIPIENT = 'arnavahuja66@gmail.com'
    }

    stages {
        stage('Stage 1: Build') {
            steps {
                // Description of the stage
                echo '''The Build stage is responsible for compiling the application code.
                It uses a build automation toolto download necessary dependencies, compile the source code, 
                and package it into a distributable format.'''
                // Example of a tool
                echo 'Example Tool: Maven'
            }
        }

        stage('Stage 2: Unit and Integration Tests') {
            steps {
                // Description of the stage
                echo '''In this stage, unit tests and integration tests are executed. 
                Unit tests verify the functionality of individual components, ensuring that the smallest pieces of code work correctly. 
                Integration tests, on the other hand, validate that different modules or services within the application interact as expected.'''
                // Example of a tool
                echo 'Example Tools: JUnit, Selenium'
            }
            post {
                always {
                    mail(
                        to: "${EMAIL_RECIPIENT}",
                        subject: "Pipeline - Unit and Integration Tests Completed",
                        body: "Stage 2 has completed. Status: ${currentBuild.currentResult}.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Stage 3: Code Analysis') {
            steps {
                // Description of the stage
                echo '''This stage scans the code to ensure it adheres to best practices and coding standards. 
                It checks for potential bugs, code smells, and vulnerabilities that may lead to poor code quality 
                or future maintenance issues.'''
                // Example of a tool
                echo 'Example Tool: SonarQube'
            }
        }

        stage('Stage 4: Security Scan') {
            steps {
                // Description of the stage
                echo '''This stage performs a security scan on the application’s dependencies and codebase to detect known vulnerabilities. 
                It ensures that the software doesnt contain security flaws that could be exploited in production environments.'''
                // Example of a tool
                echo 'Example Tool: OWASP Dependency Check'
            }
            post {
                always {
                    mail(
                        to: "${EMAIL_RECIPIENT}",
                        subject: "Pipeline - Security Scan Completed",
                        body: "Stage 4 has completed. Status: ${currentBuild.currentResult}.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Stage 5: Deploy to Staging') {
            steps {
                // Description of the stage
                echo '''In this stage, the application is deployed to a staging environment. 
                Staging environments are replicas of the production environment and allow for testing in a "production-like" setting. 
                This step ensures that the application will work as expected once deployed to the live environment.'''
                // Example of a tool
                echo 'Example Tools: AWS EC2, Docker'
            }
        }

        stage('Stage 6: Integration Tests on Staging') {
            steps {
                // Description of the stage
                echo '''After deploying to staging, integration tests are executed on the deployed application to ensure all services 
                and components work well together in the staging environment. 
                This verifies that the application behaves as expected under real-world conditions.'''
                // Example of a tool
                echo 'Example Tool: Postman'
            }
        }

        stage('Stage 7: Deploy to Production') {
            steps {
                // Description of the stage
                echo '''Once all tests have passed in the staging environment, 
                the final stage is to deploy the application to the production environment, where it becomes available to end-users.'''
                // Example of a tool:
                echo 'Example Tool: AWS EC2 or Kubernetes'
            }
        }
    }

    post {
        failure {
            mail(
                to: "${EMAIL_RECIPIENT}",
                subject: "Pipeline Failed at ${env.STAGE_NAME}",
                body: "The pipeline has failed at stage: ${env.STAGE_NAME}. Please check the logs for more details."
            )
        }
    }
}
