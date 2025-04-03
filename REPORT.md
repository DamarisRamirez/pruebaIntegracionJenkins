# Gestión del Repositorio Git

## 1. Inicialización del Repositorio Local

Se creó un nuevo repositorio local y se realizó un commit inicial con un archivo `README.md`.

### Comandos ejecutados:

```bash
# Crear una carpeta para el repositorio
mkdir pruebaIntegracionJenkins && cd pruebaIntegracionJenkins

# Inicializar el repositorio
git init

# Crear un archivo README.md
echo "# pruebaIntegracionJenkins" > README.md

# Agregar el archivo al área de staging
git add README.md

# Hacer el commit inicial
git commit -m "Commit inicial con README.md"
```

## 2. Configuración de Identidad en Git

Dado que Git requería una identidad configurada, se establecieron el nombre y el correo electrónico:

### Comandos ejecutados:

```bash
git config --global user.name "usuario"
git config --global user.email "mail"
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
git remote add origin https://github.com/DamarisRamirez/pruebaIntegracionJenkins

# Verificar la conexión
git remote -v

# Subir los cambios al repositorio remoto
git branch -M main
git push -u origin main
```

## 4. Creación de la API con Node.js y Express

Se creó una API simple que expone las rutas `/users` y `/users/:id` en el puerto `3000`.

### Comandos ejecutados:

```bash
# Inicializar el proyecto Node.js
npm init -y

# Instalar Express
npm install express

```

Se agregó el siguiente código en `app.js`:

```javascript
const express = require('express');
const app = express();
const data = require('./db.json');

app.use(express.json());

app.get('/users', (req, res) => {
  res.status(200).json(data.users);
});

app.get('/users/:id', (req, res) => {
  const user = data.users.find(u => u.id === parseInt(req.params.id, 10));
  if (user) {
    res.status(200).json(user);
  } else {
    res.status(404).json({ error: 'User not found' });
  }
});

const PORT = 3000;

app.listen(PORT, () =>
  console.log(`Servidor corriendo en http://localhost:${PORT}`)
);


module.exports = app;


## 5. Creación del Dockerfile para la API

Se creó un `Dockerfile` para construir una imagen que incluya la API  para desarrollo.

### Contenido del `Dockerfile`:

```dockerfile
# Use the official Node.js image
FROM node:16

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and install dependencies
COPY package.json ./
RUN npm install

# Copy application code
COPY . .

# Expose port 3000
EXPOSE 3000

# Run the application
CMD ["npm", "start"]
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

---

## 8. Jenkins

Para actualizar los cambios realizados en el repositorio local a GitHub, se ejecutaron los siguientes pasos:

### Contenido del `Jenkinsfile`:

```bash

```
