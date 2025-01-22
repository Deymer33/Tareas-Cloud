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

# Etapa 1: Construcción
FROM node:18 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .


# Etapa 2: Producción
FROM node:18-alpine
WORKDIR /app
COPY --from=build /app/index.js ./
COPY --from=build /app/package.json ./

# Exponer el puerto y ejecutar la aplicación
EXPOSE 3000
CMD ["node", "index.js"]