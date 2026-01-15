pipeline {
  agent any

  tools {
    // Asegúrate de tener este JDK configurado en Jenkins
    jdk 'temurin-17'
  }

  environment {
    ANDROID_SDK_ROOT = "${env.JENKINS_HOME}\\android-sdk"
    ANDROID_HOME     = "${env.JENKINS_HOME}\\android-sdk"
    SDKMANAGER       = "${env.JENKINS_HOME}\\android-sdk\\cmdline-tools\\latest\\bin\\sdkmanager.bat"
  }

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Prepare Android SDK') {
      steps {
        bat '''
        if not exist "%ANDROID_SDK_ROOT%" (
          echo Creating Android SDK directory
          mkdir "%ANDROID_SDK_ROOT%"
        )

        if not exist "%ANDROID_SDK_ROOT%\\cmdline-tools\\latest" (
          echo Downloading Android SDK Command Line Tools...
          curl -L -o cmdline-tools.zip https://dl.google.com/android/repository/commandlinetools-win-11076708_latest.zip

          tar -xf cmdline-tools.zip

          if not exist "%ANDROID_SDK_ROOT%\\cmdline-tools" (
            mkdir "%ANDROID_SDK_ROOT%\\cmdline-tools"
          )

          move cmdline-tools "%ANDROID_SDK_ROOT%\\cmdline-tools\\latest"
        ) else (
          echo Android SDK Command Line Tools already present
        )
        '''
      }
    }

    stage('Accept Licenses & Install SDK') {
      steps {
        bat '''
        echo Accepting licenses and installing SDK packages...

        echo y | "%SDKMANAGER%" --sdk_root="%ANDROID_SDK_ROOT%" ^
          "platform-tools" ^
          "platforms;android-34" ^
          "build-tools;34.0.0"
        '''
      }
    }

    stage('Build') {
      steps {
        bat '''
        echo Starting Gradle build...
        gradlew build
        '''
      }
    }
  }

  post {
    success {
      echo 'Android build completed successfully'
    }
    failure {
      echo 'Android build failed'
    }
  }
}
