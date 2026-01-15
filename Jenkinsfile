pipeline {
  agent any

  environment {
    ANDROID_SDK_ROOT = "${env.JENKINS_HOME}\\android-sdk"
    ANDROID_HOME     = "${env.JENKINS_HOME}\\android-sdk"
    SDKMANAGER       = "${env.ANDROID_SDK_ROOT}\\cmdline-tools\\latest\\bin\\sdkmanager.bat"
  }

  stages {

    stage('Prepare Android SDK') {
      steps {
        bat '''
        if not exist "%ANDROID_SDK_ROOT%" (
          mkdir "%ANDROID_SDK_ROOT%"
        )

        if not exist "%ANDROID_SDK_ROOT%\\cmdline-tools\\latest" (
          echo Downloading Android SDK Command Line Tools...
          curl -L -o cmdline-tools.zip https://dl.google.com/android/repository/commandlinetools-win-11076708_latest.zip
          tar -xf cmdline-tools.zip
          mkdir "%ANDROID_SDK_ROOT%\\cmdline-tools"
          move cmdline-tools "%ANDROID_SDK_ROOT%\\cmdline-tools\\latest"
        )
        '''
      }
    }

    stage('Accept Licenses & Install SDK') {
      steps {
        bat '''
        yes | "%SDKMANAGER%" --sdk_root="%ANDROID_SDK_ROOT%" ^
          "platform-tools" ^
          "platforms;android-34" ^
          "build-tools;34.0.0"
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
}
