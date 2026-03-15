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
                sh 'mkdir -p bin'
                sh 'javac -d bin src/*.java'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Package') {
            steps {
                echo 'Creating JAR file...'
                sh 'jar cf hello-java.jar -C bin .'
            }
        }

        stage('Prepare Package Directory') {
            steps {
                echo 'Preparing package directory for DEB...'
                sh '''
                    mkdir -p package/usr/local/bin
                    cp hello-java.jar package/usr/local/bin/
                '''
            }
        }

        stage('Build DEB using FPM') {
            steps {
                echo 'Creating .deb package with FPM...'
                sh '''
                    fpm -s dir -t deb -n hello-java -v 1.0.${BUILD_NUMBER} --prefix=/ -C package .
                '''
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
            archiveArtifacts artifacts: '*.deb, *.jar'
        }
        failure {
            echo 'Build failed. Check console output for details.'
        }
    }
}
