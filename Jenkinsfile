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

              post {
                        success {
                                // Archive build artifacts
                                archiveArtifacts artifacts: '**/*.apk', allowEmptyArchive: true, fingerprint: true
                            }
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

           stage('Distribute') {
                      steps {
                          script {
                              // Send the build to Firebase App Distribution
                              sh "firebase appdistribution:distribute app/build/outputs/apk/debug/app-debug.apk --app 1:484033308624:android:31abfd2405a664abf63bd5 --token '1//0gKSdd-qT-6-jCgYIARAAGBASNwF-L9IrJ1ku29rmy5BghSY9AVsMke0AuOoyx0etVqCHN6ARaSxEXhRECz0t2kfgtRq0W0L7OQA'"
                          }
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
