pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Preparing TechNova website'

                sh '''
                    test -s index.html
                    grep -q "TechNova Solutions" index.html
                    echo "Build successful"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Validating website content'

                sh '''
                    grep -q "Our Services" index.html
                    grep -q "About TechNova" index.html
                    grep -q "Contact Us" index.html

                    echo "All website tests passed"
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying TechNova to Apache'

                sh '''
                    install -D -m 644 index.html \
                    /var/www/html/technova/index.html
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                    test -s /var/www/html/technova/index.html

                    grep -q "Building Smarter Digital Solutions" \
                    /var/www/html/technova/index.html

                    echo "TechNova deployment verified"
                '''
            }
        }
    }

    post {
        success {
            echo 'TechNova website deployed successfully!'
        }

        failure {
            echo 'Deployment failed. Check Console Output.'
        }
    }
}
