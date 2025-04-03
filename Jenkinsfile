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
                    } catch (Exception e) {
                        error("❌ Error en la etapa de dependencias")
                    }
                }
            }
        }

        // --- ETAPA 3: EJECUTAR PRUEBAS ---
        stage('Ejecutar Pruebas') {
            options {
                timeout(time: 5, unit: 'MINUTES') // por si se queda pegado
            }
            steps {
                script {
                    try {
                        echo "🧪 Ejecutando pruebas unitarias con cobertura..."
                        bat 'npm test -- --coverage --runInBand --ci --detectOpenHandles --forceExit'
                    } catch (Exception e) {
                        error("❌ Error en la etapa de pruebas")
                    }
                }
            }
        }

        // --- ETAPA 4: CONSTRUIR Y EJECUTAR DOCKER ---
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
}
