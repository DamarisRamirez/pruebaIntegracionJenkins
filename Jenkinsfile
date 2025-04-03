pipeline {
    agent any

    environment {
        NODE_VERSION = '18.16'
    }

    stages {
        // --- ETAPA 1: CLONAR REPOSITORIO ---
        stage('Clonar Repositorio') {
            steps {
                echo "** Clonando repositorio desde GitHub **"
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
                script {
                    try {
                        echo "⚙️ Instalando dependencias..."
                        bat 'npm install'
                        bat 'npm install jest-junit --save-dev'
                    } catch (Exception e) {
                        error("❌ Error en la etapa de dependencias")
                    }
                }
            }
        }

        // --- ETAPA 3: VALIDAR API LOCAL ---
        stage('Validar API') {
            steps {
                script {
                    echo "🚀 Iniciando API local con json-server..."
                    bat 'start /B json-server --watch db.json --port 3000'
                    bat 'timeout /t 10 /nobreak'
                    bat 'curl --fail http://localhost:3000/users || exit 1'
                }
            }
        }

        // --- ETAPA 4: EJECUTAR PRUEBAS ---
        stage('Ejecutar Pruebas') {
            steps {
                script {
                    try {
                        echo "🧪 Ejecutando pruebas unitarias..."
                        bat 'npm test -- --coverage --reporters=jest-junit'
                    } catch (Exception e) {
                        error("❌ Error en la etapa de pruebas")
                    }
                }
            }
            post {
                always {
                    junit 'junit.xml'
                    archiveArtifacts artifacts: 'coverage/**/*', allowEmptyArchive: true
                }
            }
        }

        // --- ETAPA 5: CONSTRUIR Y EJECUTAR DOCKER ---
        stage('Docker') {
            steps {
                script {
                    echo "🐳 Construyendo imagen Docker..."
                    bat "docker build -t prueba_ci ."
                    echo "▶️ Ejecutando contenedor Docker..."
                    bat "docker run -d -p 3000:3000 prueba_ci"
                }
            }
        }
    }

    // --- POST-ACCIONES ---
    post {
        success {
            echo "✅ Pipeline completado con éxito"
        }

        failure {
            echo "❌ El pipeline ha fallado"
            emailext(
                subject: "🚨 Pipeline Fallido - ${env.JOB_NAME}",
                body: "Las pruebas fallaron o la API no responde. Detalles: ${env.BUILD_URL}",
                to: 'equipo@techflow.com'
            )
        }
    }
}
