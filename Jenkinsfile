pipeline {
  agent any

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
          mkdir "%ANDROID_SDK_ROOT%"
        )

        if not exist "%ANDROID_SDK_ROOT%\\cmdline-tools\\latest" (
          curl -L -o cmdline-tools.zip https://dl.google.com/android/repository/commandlinetools-win-11076708_latest.zip
          tar -xf cmdline-tools.zip
          mkdir "%ANDROID_SDK_ROOT%\\cmdline-tools"
          move cmdline-tools "%ANDROID_SDK_ROOT%\\cmdline-tools\\latest"
        )
        '''
      }
    }

    stage('Accept ALL SDK Licenses') {
      steps {
        bat '''
        echo y | "%SDKMANAGER%" --sdk_root="%ANDROID_SDK_ROOT%" --licenses
        '''
      }
    }

    stage('Install Required SDK Packages') {
      steps {
        bat '''
        "%SDKMANAGER%" --sdk_root="%ANDROID_SDK_ROOT%" ^
          "platform-tools" ^
          "platforms;android-35" ^
          "build-tools;35.0.0"
        '''
      }
    }

    stage('Build') {
      steps {
        bat '''
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

