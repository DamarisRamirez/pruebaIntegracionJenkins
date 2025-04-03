pipeline {
    agent any

    stages {
        // --- ETAPA 1: CLONAR REPOSITORIO ---
        stage('Clonar Código') {
            steps {
                checkout([ 
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/DamarisRamirez/pruebaIntegracionJenkins.git']]
                ])
            }
        }

        // --- ETAPA 2: INSTALAR DEPENDENCIAS ---
        stage('Instalar Dependencias') {
            steps {
                bat 'npm install'
                bat 'npm install jest-junit --save-dev' // Para reportes JUnit
            }
        }

        // --- ETAPA 3: INICIAR Y VALIDAR API ---
        stage('Validar API') {
            steps {
                script {
                    bat 'start /B json-server --watch db.json --port 3000' // Inicia servidor
                    bat 'timeout /t 10 /nobreak' // Espera 10 segundos
                    bat 'curl --fail http://localhost:3000/users || exit 1' // Valida respuesta
                }
            }
        }

        // --- ETAPA 4: EJECUTAR PRUEBAS ---
        stage('Ejecutar Pruebas') {
            steps {
                bat 'npm test -- --coverage --reporters=jest-junit' // Ejecuta pruebas con reportes
            }
            post {
                always {
                    junit 'junit.xml' // Archiva resultados JUnit
                    archiveArtifacts artifacts: 'coverage/**/*', allowEmptyArchive: true // Reporte de cobertura
                }
            }
        }
    }

    // --- POST-ACCIONES ---
    post {
        failure {
            emailext(
                subject: "🚨 Pipeline Fallido - ${env.JOB_NAME}",
                body: "Las pruebas fallaron o la API no responde. Detalles: ${env.BUILD_URL}",
                to: 'equipo@techflow.com'
            )
        }
    }
}