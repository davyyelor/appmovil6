pipeline {
  agent any

  environment {
    ANDROID_HOME     = 'C:\\Users\\delorzagabilondo\\AppData\\Local\\Android\\Sdk'
    ANDROID_SDK_ROOT = 'C:\\Users\\delorzagabilondo\\AppData\\Local\\Android\\Sdk'
    PATH = "${env.ANDROID_HOME}\\cmdline-tools\\latest\\bin;" +
           "${env.ANDROID_HOME}\\platform-tools;" +
           "${env.PATH}"
  }

  stages {
    stage('Checkout & Build') {
      steps {
        ws('C:/jk/pruebaBackstagejenkins') {

          checkout scm

          bat 'git config core.longpaths true'

          // Indicamos explícitamente a Gradle dónde está el SDK
          bat "echo sdk.dir=${env.ANDROID_HOME.replace('\\', '/')} > local.properties"

          bat 'gradlew.bat build'
        }
      }
    }
  }
}
