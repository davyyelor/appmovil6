pipeline {
    agent any

    stages {
        stage('Checkout & Build') {
            steps {
                // Esto crea una carpeta corta para evitar el límite de 260 caracteres
                ws("C:/jk/${env.JOB_NAME}") {
                    bat 'git config core.longpaths true'
                    checkout scm
                    bat './gradlew build'
                }
            }
        }
    }

}
