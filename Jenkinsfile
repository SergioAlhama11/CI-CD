pipeline {
    agent any

    stages {
        stage('Build'){
            steps {
                echo 'Construyendo la app...'
                git 'https://github.com/SergioAlhama11/CI-CD.git'
            }
        }

        stage('Test') {
            steps {
                echo 'Ejecutando tests...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy'){
            steps {
                echo 'Desplegando app en Raspberry Pi...'
                
                sh '''
                if lsof -ti:8080 | grep -q .; then
                    kill $(lsof -ti:8080)
                fi
                '''

                sh 'nohup java -jar target/quarkus-app/quarkus-run.jar > app.log 2>&1 &'
            }
        }
    }
}