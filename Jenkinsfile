pipeline {
    agent any

    environment {
        // This fills the ${docker-registry} placeholder in your yaml file
        docker_registry = "cicdcicd40"
        APP_NAME = "my-app"
    }

    stages {
        stage('Build') {
            steps {
                echo "Building application image for ${docker_registry}..."
                // Build only the app service defined in your YAML
                sh "docker compose build my-app"
            }
        }

        stage('Test') {
            steps {
                echo "Starting MongoDB for tests..."
                // Start the database in detached mode
                sh "docker compose up -d mongodb"

                echo "Running integration tests..."
                // Executes tests inside the app container
                sh "docker compose run my-app npm test"
            }
            post {
                always {
                    echo "Cleaning up containers..."
                    sh "docker compose down"
                }
            }
        }

        stage('Deploy') {
            steps {
                // Placeholder for future deployment logic
                echo "DEPLOYMENT PLACEHOLDER: Image is built and tested."
                echo "To push this image manually, run: docker push ${docker_registry}/${APP_NAME}:latest"
            }
        }
    }
}
