pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling Java files...'
                // Make sure you have a folder named 'bin' or it will be created automatically
                sh 'mkdir -p bin'
                sh 'javac -d bin src/*.java'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add test commands here if you have tests
                // Example: sh 'java -cp bin org.junit.runner.JUnitCore MyTestClass'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging (optional)...'
                // Example: create a jar file
                sh 'jar cf hello-java.jar -C bin .'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Check console output for details.'
        }
    }
}
