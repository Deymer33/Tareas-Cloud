Tarea Servicios de Cómputo en la Nube - Ejemplos Prácticos

## Preguntas:

1. Máquinas Virtuales: ¿Qué tipo de aplicaciones podrías ejecutar en una máquina virtual (AWS EC2, Azure Virtual Machines, Google Compute Engine)? Da al menos 3 ejemplos concretos y explica por qué una máquina virtual sería adecuada para cada caso.

se pueden correr multiple tipo de aplicaciones siempre y cuando cumpla con los recursos asignados en el entorno y que sea compatible con el sistema operativo 

los tipos de aplicaciones que podriamos correr seria;

	--Sitios web: Usando servidores como Apache, Nginx, o IIS
	--plataformas CMS por ejemplo wordpress
	--bases de datos relacionales como no relacionales
	--aplicaciones empresariales tipo ERP  y CRM 
	--entornos de pruebas 
	--pruebas en CI/CD pipelines
	-- firewall virtuales 
	--servidores vpn 
	--contenedores y orquestacion como docker y kubernetes AWS ECS/EKS, Azure AKS, Google GKE. 

ejemplo donde es clave su uso:

1.Un startup quiere desplegar una aplicación web en Python usando Django y una base de datos PostgreSQL para gestionar usuarios y contenido.

es recomedable usar una maquina virtual por la escalabilidad ya que permiten ajustar facilmente la cantidad de recursos a utilizar dando un optimo desesmpeño en el sistema y tambien ayudando consumir en gastos lo necesareo. el aislamiento es muy importante en este caso ya que garantiza que cada parte del sistema trabaje de manera independiente reduciendo el riesgo de problemas con otros sistemas.

2.Una empresa de desarrollo necesita probar su aplicación en múltiples sistemas operativos, como Windows Server, Ubuntu.

Versatilidad ya que Puedes lanzar diferentes máquinas virtuales con distintos sistemas operativos en minutos, sin necesidad de hardware físico dedicado para cada uno tambien En lugar de mantener múltiples servidores físicos, puedes usar máquinas virtuales por el tiempo exacto que las necesitas permitiendo la reducion de costos

3.Una empresa de comercio electrónico necesita un servidor para alojar una base de datos PostgreSQL que gestione millones de transacciones diarias.

La base de datos puede ejecutarse en una máquina virtual dedicada, separada de otros servicios, lo que mejora la seguridad y el rendimiento. puede asegurarse tambien la escalabilidad ya que si el volumen de datos crece o la carga aumenta, es sencillo aumentar los recursos de la máquina

---

2. Funciones Serverless: ¿Qué es una función serverless (AWS Lambda, Azure Functions, Google Cloud Functions)? Explica su funcionamiento y da al menos 2 ejemplos de casos de uso.

una funcion serverles significa sin servidor ose que te permite administrar datos e integrar aplicaciones, todo sin tener que administrar servidores.todo disponible para desplegarar y no preocuparse por el consumo de recurso ya que estas asignaciones se haran automaticamente por el servico de la nube en cuestion.

ejemplo1: Una aplicación web permite a los usuarios cargar imágenes de perfil. Al cargar una imagen, se debe redimensionar y optimizar automáticamente para diferentes tamaños (miniatura, tamaño estándar, etc.)al momento de subir la imagen al servicio por ejempo amazonS3 

Una función Lambda (serverles funciona en lambda en amazone) se activa automáticamente cuando se detecta el archivo cargado. Esta función:

	-Redimensiona la imagen a diferentes tamaños.
	-Optimiza la calidad para reducir el peso del archivo etc.
No necesitas mantener servidores siempre activos. La función se ejecuta solo cuando hay una nueva imagen.


ejmplo2: Un sistema de e-commerce necesita enviar notificaciones por correo electrónico o mensajes de texto cuando se completa un pedido
-Evento desencadenante: Un cliente realiza un pedido y se registra en la base de datos (por ejemplo, un registro nuevo en DynamoDB o una actualización en Firestore).
-Función serverless: Una función (por ejemplo, en Google Cloud Functions) se activa al detectar el evento y:
    - Genera un correo electrónico personalizado con los detalles del pedido.
	-asi solo consumes recursos cuando se realiza un pedido
	-la Integración es sencilla con sistemas existentes

---



3. Comparación: ¿Qué diferencias hay entre usar una máquina virtual y una función serverless? ¿En qué situaciones usarías cada una?  Considera factores como control, escalabilidad, costo y facilidad de uso.

las maquinas virtuales Ofrecen control total sobre el sistema operativo, configuración y aplicaciones instaladas. Ideal para entornos personalizados ademas permite ejecutar aplicaciones complejas, como bases de datos, servidores web y aplicaciones legacy. Adecuada para aplicaciones con múltiples dependencias o que requieren control total del entorno en cambio en una funcion serverless es Limitado al código y configuración de la función; el entorno está gestionado por el proveedor. Escala automáticamente según la carga; ideal para manejar picos impredecibles, Diseñado para tareas específicas o eventos puntuales; no adecuado para aplicaciones de larga ejecución y su tiempo de inicio rápido, generalmente en milisegundos

yo usaria maquinas virtuales para servidores de bases de datos o aplicaciones con muchas dependencias y tareas continuas por mucho tiempo y las funciones serverless para tareas muy especificas y a cuando conozco que habra intermitencia en el trabajo o cargas impredecibles  

---

4. Sitio Web Sencillo: Si tuvieras que construir un sitio web sencillo, ¿qué servicio de cómputo usarías (máquina virtual o función serverless) y por qué?  Justifica tu elección.

Utilizaaraia una funcion serverles ya que seria algo de uso momentaneo y no tendria mucha carga y si tubiera un pico de uso el mismo servicio se encargaria de la gestion permitiendo flexiblidad y reduciendo los costos de uso 

---

5. Tipos de Instancias (AWS EC2): Investiga al menos 3 tipos de instancias de Amazon EC2 (ej. t2.micro, m5.large, etc.) y explica para qué se utiliza cada una. Considera factores como capacidad de procesamiento, memoria RAM y costo.

-m5a.xlarge: tiene 4 cpu virtual, 16 memoria (Gib) ofrecen hasta un 10 % de ahorro en costos con respecto a otros tipos de instancias comparables. Con las instancias M5ad

Casos de uso

Bases de datos pequeñas y medianas, tareas de procesamiento de datos que requieren memoria adicional, flotas de almacenamiento en caché y ejecución de servidores backend para SAP, Microsoft SharePoint, informática en clústeres y otras aplicaciones empresariales.

-t3.xlarge: tiene 4 cpu virtual, 16 memoria (Gib)proporciona un nivel de rendimiento de la CPU de referencia con la capacidad de ampliar el uso de la CPU en cualquier momento durante el tiempo que sea necesario. Las instancias T3 ofrecen un equilibrio entre recursos de computación, de memoria y de red, y están diseñadas para aplicaciones con un uso moderado de la CPU que experimentan picos temporales de uso.

Casos de uso:

Microservicios, aplicaciones interactivas con baja latencia, bases de datos de tamaño pequeño y mediano, escritorios virtuales, entornos de desarrollo, repositorios de código y aplicaciones críticas para la empresa

---

6. Activación de Funciones Serverless: ¿Cómo se activa una función serverless? Explica los diferentes tipos de triggers o eventos que pueden iniciar la ejecución de una función.

Una función serverless se activa en respuesta a triggers o eventos específicos configurados en el entorno cloud. Estos eventos indican al proveedor de la nube que debe ejecutar el código asociado a la función

-Eventos de Almacenamiento
-Eventos HTTP o API Gateway
-Eventos de Base de Datos
-Eventos de Mensajería y Colas: Mensajes en cola o sistema de pub/sub
-Eventos de Cambios en Infraestructura: En AWS CloudFormation o Google Cloud Deployment Manager, una función puede activarse cuando se completa un despliegue para realizar tareas posteriores, como enviar notificaciones.
-Integraciones Personalizadas, Ejemplo: Una función se activa cuando se recibe una webhook de Stripe (para pagos) 

---

7. Herramientas de Despliegue: Investiga al menos 2 herramientas que se utilizan para desplegar aplicaciones en la nube (ej. AWS Elastic Beanstalk, Azure DevOps, Google Cloud Build). Describe brevemente sus funciones.

AWS Elastic Beanstalk es un servicio que facilita la implementación y gestión de aplicaciones web en la nube de AWS. Permite a los desarrolladores cargar su código y Elastic Beanstalk se encarga automáticamente del aprovisionamiento de recursos, balanceo de carga, escalado automático y monitoreo del estado de la aplicación. Es compatible con varios lenguajes de programación y plataformas, incluyendo Java, .NET, PHP, Node.js, Python, Ruby, Go y Docker.

Azure DevOps es un conjunto de herramientas y servicios que ayudan en la administración del ciclo de vida de proyectos de desarrollo de software. Proporciona una plataforma para la colaboración entre equipos, facilitando la planificación, desarrollo, entrega y operación de aplicaciones.
