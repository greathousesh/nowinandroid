pipeline {
    agent any

    environment {
        ANDROID_HOME = '/opt/android-sdk'
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'

        PATH = "${JAVA_HOME}/bin:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools:${env.PATH}"
    }

    stages {

        stage('Environment') {
            steps {
                sh '''
                    java -version
                    ./gradlew --version
                '''
            }
        }

        stage('Unit Test') {
            steps {
                sh '''
                    chmod +x gradlew
                    ./gradlew testDebugUnitTest
                '''
            }
        }

        stage('Build Debug APK') {
            steps {
                sh '''
                    ./gradlew assembleDebug
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts(
                artifacts: 'app/build/outputs/apk/**/*.apk',
                fingerprint: true
            )
        }
    }
}