stage('Checkout & Build') {
  steps {
    ws('C:/jk/pruebaBackstagejenkins') {

      checkout scm

      bat 'git config core.longpaths true'

      bat '''
      powershell -Command ^
        "Set-Content -Path local.properties -Value 'sdk.dir=C:/Users/delorzagabilondo/AppData/Local/Android/Sdk' -NoNewline"
      '''

      bat 'gradlew.bat build'
    }
  }
}
