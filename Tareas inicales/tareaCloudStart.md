**que son los cold starts de Lambda para AWS**:


Los **cold starts** en AWS Lambda se refieren al tiempo adicional que tarda en inicializarse una función Lambda cuando se invoca después de haber estado inactiva durante un período de tiempo. AWS Lambda ejecuta funciones dentro de contenedores que se asignan dinámicamente. Si no hay un contenedor existente listo para procesar la solicitud aws debera crear un contenedor para ejecutar la funcion tambien tiene que descargar el código y las dependencias de la función desde S3, inicializar el entorno e iniciar el runtime.