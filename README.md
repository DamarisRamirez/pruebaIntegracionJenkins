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

1. Construir la imagen: `docker build -t desafio_jenkins`
2. Ejecutar el contenedor: `docker run -p 3000:3000 desafio_jenkins`

## Reporte
- En el archivo REPORT.md se encuentra la explicación de las configuraciones realizadas.
- En la carpeta `documents` en la raiz del proyecto se encuentran 2 archivos:
1. capturas.pdf: Contiene las capturas de pantalla del pipeline configurado en Jenkins.
2. resultadosJenkins.pdf: Contiene el resultado por consola arrojado por Jenkins al realizar el pipeline.

## Integrantes
- Claudia Ortiz
- Rene Parada
- Damaris Ramirez
- Carolina Rojas
- Henry Saldaña