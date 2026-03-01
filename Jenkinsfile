pipeline {
    agent any
    tools {
        maven 'M3'
    }
    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Zersource/DeBasedeDatos-------S7.git'
            }
        }
        stage('Build Application - Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Docker Image') {
            steps {
                sh 'docker build -t imagen_vehiculos .'
            }
        }
        stage('Deployment') {
            steps {
                sh '''
                    docker stop contenedor_sucursal || true
                    docker rm contenedor_sucursal || true
                    docker run -d -p 9090:8080 --name contenedor_sucursal --link mysql-vehiculos:mysql-vehiculos imagen_vehiculos
                '''
            }
        }
    }
}
