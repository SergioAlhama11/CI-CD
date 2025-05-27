pipeline {
    agent any
    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout') {
            steps {
                checkout scm  // Esto clona el repo en el nodo Jenkins
            }
        }

        stage('Check workspace') {
            steps {
                sh 'pwd'
                sh 'ls -la'
            }
        }
        
        stage('Build') {
            steps {
                echo 'Construyendo la app...'
                agent {
                    docker {
                        image 'maven:3.8.5-openjdk-17'
                        args '-v /var/run/docker.sock:/var/run/docker.sock' // Para poder usar Docker dentro del contenedor si necesitas
                    }
                }

                // El código ya está clonado por Jenkins desde el SCM configurado en el job
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Ejecutando tests...'
                // Aquí podrías ejecutar tests reales si quieres
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Desplegando app en Raspberry Pi...'

                sh '''
                # Matar proceso en puerto 8080 si existe
                if lsof -ti:8080 | grep -q .; then
                    kill $(lsof -ti:8080)
                fi
                '''

                sh 'nohup java -jar target/quarkus-app/quarkus-run.jar > app.log 2>&1 &'
            }
        }
    }
}