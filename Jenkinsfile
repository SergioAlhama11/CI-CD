pipeline {
    agent any

    stages {
        stage('Build'){
            steps {
                echo 'Construyendo la app...'
            }
        }

        stage('Test') {
            steps {
                echo 'Ejecutando tests...'
            }
        }

        stage('Deploy'){
            steps {
                echo 'Desplegando app en Raspberry Pi...'
            }
        }
    }
}