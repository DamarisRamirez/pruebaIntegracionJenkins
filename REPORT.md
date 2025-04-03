# Pipeline Execution Report

## Summary

Este reporte constata los pasos realizados para configurar y ejecutar un pipeline CI/CD con Jenkins

## Steps

1. **Git Repository Management**  
     
- Se inicializó un repositorio local de git y se conectó a GitHub



2. **Docker Integration**  
     
- Se crea archivo Dockerfile 

   

3. **Jenkins Configuration**  
Se configura Jenkins en archivo Jenkisfile con instrucciones de:
   1. Clonación de repositorio remoto GitHub. 
   2. Instalación de dependencias (npm install).
   3. Ejecutar las pruebas automatizadas (npm test).
   4. Construcción de una imagen Docker a partir del Dockerfile

### Clonar el Repositorio

- Jenkins obtiene el código desde el repositorio usando `checkout scm`.

 

### Instalar Dependencias

- Ejecuta `npm install` para instalar las dependencias del proyecto.

 

### Ejecutar Pruebas

- Ejecuta `npm test` para correr las pruebas automatizadas.

 

### Construir y Ejecutar Docker

- Construye una imagen con `docker build -t desafio_jenkins .`.

- Ejecuta el contenedor con `docker run -p 3000:3000 desafio_jenkins`.

 

### Post-Ejecución

- Si el pipeline es exitoso, muestra "Pipeline completado con éxito".

- Si falla en algún paso, muestra "El pipeline ha fallado".

## Issues Encountered

- \[Optional section for issues\]

## Results

- Resultados visibles en documento pdf ./documents/resultadosJenkins.pdf

