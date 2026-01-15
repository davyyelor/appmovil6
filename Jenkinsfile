pipeline {
    agent any
    environment {
        // Definim la ruta on has instal·lat l'SDK d'Android
        ANDROID_HOME = 'C:\\android-sdk'
        // Afegim les eines al PATH per si Gradle les necessita directament
        PATH = "${env.ANDROID_HOME}\\cmdline-tools\\latest\\bin;${env.ANDROID_HOME}\\platform-tools;${env.PATH}"
    }
 
    stages {
        stage('Checkout & Build') {
            steps {
                ws('C:/jk/pruebaBackstagejenkins') {
                    // Checkout del codi
                    checkout scm
                    // Corregir permisos o configuracions de rutes llargues en Windows
                    bat 'git config core.longpaths true'
                    // Creem un fitxer local.properties dinàmicament si no existeix
                    // Això indica a Gradle exactament on és l'SDK
                    bat "echo sdk.dir=${env.ANDROID_HOME.replace('\\', '/')} > local.properties"
                    // Execució del build
                    bat 'gradlew.bat build'
                }
            }
        }
    }
}
