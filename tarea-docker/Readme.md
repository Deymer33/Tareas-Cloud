**Optimizar una Imagen Docker Multi-Stage** En esta tarea, optimizaremos una imagen Docker existente utilizando construcciones multi-stage. El objetivo es reducir el tamaño de la imagen final, lo que resulta en descargas más rápidas, menor uso de almacenamiento e **mejorada seguridad**. 


paso numero 1: instalamos la imagen sugerida en la actividad usando sudo docker pull node:18.

```zsh
sudo docker pull node:18
[sudo] password for deimer: 
18: Pulling from library/node
fd0410a2d1ae: Pull complete 
bf571be90f05: Pull complete 
684a51896c82: Pull complete 
fbf93b646d6b: Pull complete 
583b47bebcf3: Pull complete 
d00a3c3f5975: Pull complete 
5329bde7723a: Pull complete 
c3a9b0d4a636: Pull complete 
Digest: sha256:8b7f2b36c945174b27fe833689fcc47b78dd47de0eda2d6e868e6e4ec2c63ae0
Status: Downloaded newer image for node:18
docker.io/library/node:18
```

luego verificamos el tamaño de la imagen descargada:

```zsh
docker images node:18
[sudo] password for deimer: 
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
node         18        613ec9ba1740   2 months ago   1.09GB
```


creamos un proyecto y lo inicializamos: 

```zsh
node index.js
Server running at http://localhost:3000/
```
continuamos construyendo el dockerfile para esta aplicacion y pegando el siguente contenido en el docker file 

```
# Usar la imagen base de Node.js 18
FROM node:18

# Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar el archivo package.json y package-lock.json
# (Esto copia tanto `package.json`, que lista las dependencias del proyecto,
# como `package-lock.json`, que bloquea las versiones específicas de esas dependencias
# para garantizar compilaciones consistentes).
COPY package*.json ./

# Instalar las dependencias
RUN npm install

# Copiar el resto de los archivos de la aplicación
# (Esto copia todos los demás archivos y carpetas del directorio actual en tu máquina
# al directorio `/app` dentro del contenedor).
COPY . .

# Exponer el puerto en el que la aplicación escucha
EXPOSE 3000

# Comando para ejecutar la aplicación
CMD ["node", "index.js"]
```

luego de crear la imagen con el comando **docker build -t node-hello-world:original  .**
procedemos a verficar la correcta creacion de la imagen: 

```zsh
docker images                              
REPOSITORY         TAG        IMAGE ID       CREATED          SIZE
node-hello-world   original   264a014eadaf   13 seconds ago   1.09GB
node               18         613ec9ba1740   2 months ago     1.09GB
```

ejecutamos el contenedor con el comando **docker run -p 3000:3000 node-hello-world:original**  y verificamos que funciona correctamente.

ahora construiremos la imagen optimizada con el comando **docker build -t node-hello-world:optimized .(modficandio el dockerfile por etapas primero)** y observamos que tanto ha bajado el peso de la imagen.

```zsh
docker images          
REPOSITORY         TAG         IMAGE ID       CREATED          SIZE
node-hello-world   optimized   ed637f1c8a6e   59 seconds ago   127MB
node-hello-world   original    264a014eadaf   43 minutes ago   1.09GB
node               18-alpine   dcbf7b337595   13 hours ago     127MB
node               18          613ec9ba1740   2 months ago     1.09GB
```


**observamos una reducion de mas de una giga de almacenamiento haciendola mas ligera y segura para su uso**