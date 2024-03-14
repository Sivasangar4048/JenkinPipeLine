pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from your version control system (e.g., Git)
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Set up Android SDK
                sh 'export ANDROID_SDK_ROOT=/Users/rentorzo/Library/Android/sdk'

                // Build the Android application
                sh './gradlew assembleDebug'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh './gradlew testDebugUnitTest'

                // Run instrumented tests (UI tests)
                sh './gradlew connectedAndroidTest'
            }
        }

    }

    post {
        always {
            // Clean up any temporary files or resources
            cleanWs()
        }
    }
}
