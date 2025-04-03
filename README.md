# Proyecto API de Tareas

Este proyecto muestra una API Node.js sencilla para la administración de tareas, integrada con Docker para contenerización y Jenkins para el pipeline de CI/CD.

## Características

- Listar todas las tareas
- Obtener la tarea por ID

## Ejecución local

1. Instalar dependencias: `npm install`
2. Iniciar el servidor: `npm start`
3. Ejecutar las pruebas: `npm test`

## Ejecución con Docker

1. Construir la imagen: `docker build -t prueba_ci`
2. Ejecutar el contenedor: `docker run -p 3000:3000 prueba_ci`

## Reporte
- En el archivo REPORT.md se encuentra la explicación de las configuraciones realizadas.

## Integrantes
- Rodrigo Aravena
- Sebastian Huanca
- Damaris Ramirez
- Carolina Rojas
- Daniel Rojas