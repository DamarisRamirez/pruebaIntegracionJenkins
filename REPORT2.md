# Gestión del Repositorio Git

## 1. Inicialización del Repositorio Local

Se creó un nuevo repositorio local y se realizó un commit inicial con un archivo `README.md`.

### Comandos ejecutados:

```bash
# Crear una carpeta para el repositorio
mkdir mi_proyecto && cd mi_proyecto

# Inicializar el repositorio
git init

# Crear un archivo README.md
echo "# Mi Proyecto" > README.md

# Agregar el archivo al área de staging
git add README.md

# Hacer el commit inicial
git commit -m "Commit inicial con README.md"
```

## 2. Configuración de Identidad en Git

Dado que Git requería una identidad configurada, se establecieron el nombre y el correo electrónico:

### Comandos ejecutados:

```bash
git config --global user.name "rodaravena9"
git config --global user.email "rodaravena9@gmail.com"
```

Se verificó la configuración con:

```bash
git config --list
```

## 3. Creación y Conexión con un Repositorio Remoto en GitHub

1. Se creó un nuevo repositorio en GitHub (sin inicializar con archivos adicionales).
2. Se obtuvo la URL del repositorio y se vinculó al repositorio local.

### Comandos ejecutados:

```bash
# Agregar el repositorio remoto
git remote add origin https://github.com/usuario/mi_proyecto.git

# Verificar la conexión
git remote -v

# Subir los cambios al repositorio remoto
git branch -M main
git push -u origin main
```

## 4. Creación de la API con Node.js y Express

Se creó una API simple que expone las rutas `/tasks` y `/tasks/:id` en el puerto `3000`.

### Comandos ejecutados:

```bash
# Inicializar el proyecto Node.js
npm init -y

# Instalar Express
npm install express

# Instalar nodemon para desarrollo
npm install --save-dev nodemon
```

Se agregó el siguiente código en `server.js`:

```javascript
const express = require("express");
const app = express();
const port = 3000;

// Middleware para parsear JSON
app.use(express.json());

// Datos simulados
let tasks = [
  { id: 1, name: "Tarea 1" },
  { id: 2, name: "Tarea 2" },
];

// Ruta para obtener todas las tareas
app.get("/tasks", (req, res) => {
  res.json(tasks);
});

// Ruta para obtener una tarea por ID
app.get("/tasks/:id", (req, res) => {
  const task = tasks.find((t) => t.id === parseInt(req.params.id));
  if (task) {
    res.json(task);
  } else {
    res.status(404).json({ message: "Tarea no encontrada" });
  }
});

// Iniciar el servidor
app.listen(port, () => {
  console.log(`API corriendo en http://localhost:${port}`);
});
```

## 5. Creación del Dockerfile para la API

Se creó un `Dockerfile` para construir una imagen que incluya la API y nodemon para desarrollo.

### Contenido del `Dockerfile`:

```dockerfile
# Usa una imagen base de Node.js
FROM node:18

# Establece el directorio de trabajo en el contenedor
WORKDIR /app

# Copia package.json y package-lock.json
COPY package*.json ./

# Instala las dependencias incluyendo nodemon
RUN npm install

# Copia el resto del código de la aplicación
COPY . .

# Expone el puerto 3000 para acceder a la API
EXPOSE 3000

# Comando para ejecutar la aplicación en modo desarrollo con nodemon
CMD ["npm", "run", "dev"]
```

---

## 7. Actualización en GitHub

Para actualizar los cambios realizados en el repositorio local a GitHub, se ejecutaron los siguientes pasos:

### Comandos ejecutados:

```bash
# Verificar el estado de los archivos
git status

# Agregar todos los cambios al área de staging
git add .

# Realizar un commit con un mensaje descriptivo
git commit -m "Actualización del report.md con avances en la API y Dockerfile"

# Subir los cambios al repositorio remoto en GitHub
git push origin main
```
