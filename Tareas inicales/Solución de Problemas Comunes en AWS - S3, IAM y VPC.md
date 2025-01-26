**Objetivo:** Investigar y comprender los problemas más comunes que se presentan en S3, IAM y VPC, y sus respectivas soluciones.


**Ejemplo de estructura (para un problema en S3):**

- S3 (Simple Storage Service)

- Problema Común 1: Bucket S3 Público con Datos Sensibles

*   Descripción del Problema: Un bucket S3 está configurado como público, permitiendo el acceso a todos los usuarios de Internet, incluyendo datos sensibles.
*   Impacto: Exposición de datos a personas no autorizadas.  Riesgo de multas por incumplimiento de normativas de seguridad.  Pérdida de reputación.
*   Solución/es:
    1.  Desactivar el acceso público al bucket usando la consola de AWS o la AWS CLI.
    2.  Utilizar políticas de bucket para restringir el acceso a usuarios autorizados.
    3.  Activar el cifrado en reposo para proteger los datos.

- Mejores Prácticas para S3
1. Usar políticas de buckets para restringir el acceso a los datos.
2. Activar el cifrado en reposo y en tránsito para proteger la información.


**ervicios y Tópicos:** * **S3 (Simple Storage Service):** 

* **Acceso público a buckets:** 
	- El acceso público se otorga a buckets y objetos a través de listas de control de acceso (ACL),políticas de bucket o ambas. Para ayudarlo a administrar el acceso público a los recursos de AmazonS3, Amazon S3 proporciona configuraciones para bloquear el acceso público. La configuración debloqueo de acceso público de Amazon S3 puede anular políticas de buckets y ACL para que puedaaplicar al acceso público límites uniformes a dichos recursos.

* **Cifrado de datos:**
	* descripcion:  actualmente exite el cifrado del lado del servidor y del lado del cliente en aws s3. todos los buckets de Amazon S3 tienen el cifrado configurado de forma predeterminada y todos los objetos nuevos cargados en un bucket de S3 se cifran automáticamente en reposo. El cifrado del lado del servidor con claves administradas de Amazon S3 (SSE-S3) es la configuración de cifrado predeterminada para cada bucket de Amazon S3.

* **Control de versiones:** 
	* descripcion: Puede usar el control de versiones de S3 para conservar diversas variantes de un objeto en el mismo bucket. Puede utilizar el control de versiones de S3 para conservar, recuperar y restaurar todas las versiones de los objetos almacenados en su bucket de . Puede recuperarse fácilmente de accionesno deseadas del usuario y de errores de la aplicación.

* **Costos inesperados:** 
	* descripcion: puede ser por varios factores entre ellos uso excesivo de almacenamiento: Carga de datos que exceden los límites esperados o transferencia de datos:Cargos por tráfico saliente, especialmente al transferir datos fuera de AWS
	 - impacto: Incremento significativo en la factura mensual de AWS, superando el presupuesto planeado y Pérdida de visibilidad sobre el consumo de recursos.
	 - soluciones: habilitar alertas de costos y presupuestos Configurar presupuestos en AWS Budgets para recibir notificaciones al acercarse a los límites establecidos y/o Mover datos poco usados a clases como S3 Intelligent-Tiering, Glacier o Glacier Deep Archive.
---


* **IAM (Identity and Access Management):** 

* **Usuarios y roles con demasiados permisos: **
	* descricion: En AWS IAM, los usuarios y roles tienen asignados más permisos de los necesarios (esto se conoce como **sobreprivilegio**). Esto ocurre cuando se otorgan políticas demasiado amplias (por ejemplo, `"Action": "*"` o `"Resource": "*"`) en lugar de seguir el principio de **mínimo privilegio**.
	* Impacto: Riesgo de seguridad Si un usuario o rol es comprometido, el atacante tendrá acceso a más recursos y servicios de los necesarios.
	 Violaciones de cumplimiento: Muchas normativas (como GDPR, HIPAA, etc.) requieren que los permisos estén restringidos a lo estrictamente necesario
	 Errores accidentales: Usuarios con demasiados permisos podrían eliminar o modificar recursos críticos por error.
    * **Solución:**  Revisar y ajustar políticas:Usa herramientas como IAM Access Analyzer para identificar permisos innecesarios.
     Reemplaza políticas amplias (por ejemplo, `"Action": "*"`) con permisos específicos para cada tarea. 
     aplicar monitoreo y aduitar con AWS CloudTrail
     
* **Claves de acceso expuestas:** 
    * descripcion: Las claves de acceso de AWS (Access Key ID y Secret Access Key) pueden quedar expuestas accidentalmente, por ejemplo:
	 Subiéndolas a repositorios públicos en GitHub.
     Compartiéndolas en mensajes o correos no seguros.
    * **Impacto:** Acceso no autorizado: Un atacante puede usar las claves expuestas para acceder a tus recursos de AWS ademas podrian eliminarse o robarse datos críticos.
    * **solucion:** Revocar las claves expuestas de inmediato:
     Ve a la consola de IAM, localiza la clave expuesta y desactívala o elimínala.
     Rotar las claves de acceso: Crea nuevas claves de acceso y reemplázalas en todas las aplicaciones o servicios que las usen.
     
* **Falta de autenticación multi-factor (MFA):** 
	* descripcion: La autenticación multi-factor (MFA) no está habilitada para usuarios o roles en AWS IAM. Esto significa que solo se requiere una contraseña o una clave de acceso para autenticarse, lo que aumenta el riesgo de acceso no autorizado si las credenciales se ven comprometidas.
	* impacto: esto puede generar problemas de accesso no autorizado Si las credenciales de un usuario son robadas o adivinadas, un atacante puede acceder fácilmente a la cuenta ademas  Muchos estándares de seguridad (como GDPR, HIPAA, PCI DSS) requieren MFA para proteger el acceso a sistemas críticos
	* solucion: ir a la consola de IAM y activar el MFA para cada usuario.
	* Requerir MFA para acciones críticas: Configura políticas de IAM que exijan MFA para acciones sensibles, como cambios en políticas de seguridad, eliminación de recursos o acceso a datos confidenciales
* **Roles que se ejecutan bajo privilegios no deseados:** 
	* descripcion: Los roles de IAM tienen asignados permisos excesivos o no deseados, lo que permite a las entidades realizar acciones que no deberían poder ejecutar. Esto ocurre cuando las políticas adjuntas a los roles son demasiado amplias o no siguen el principio de mínimo privilegio.
	* impacto: Si un rol es comprometido, un atacante puede acceder a recursos o servicios críticos tambien Las aplicaciones o servicios que usan el rol podrían realizar acciones no intencionales, como eliminar recursos
	* solucion: Usa **IAM Access Analyzer** para identificar permisos innecesarios en las políticas adjuntas a los roles y Reemplaza políticas amplias (por ejemplo, `"Action": "*"`) con permisos específicos para cada tarea.

---

* **VPC (Virtual Private Cloud):**

* **Configuración incorrecta de grupos de seguridad y ACLs:**
   * descripcion: Los grupos de seguridad (Security Groups) y las listas de control de acceso (ACLs) están mal configurados, permitiendo tráfico no deseado o bloqueando tráfico legítimo. Esto ocurre cuando las reglas son demasiado permisivas (por ejemplo, permitir `0.0.0.0/0`) o demasiado restrictivas (bloqueando tráfico necesario).
   * Impacto: Exposición a ataques: Reglas demasiado permisivas pueden dejar recursos expuestos a accesos no autorizados desde Internet.
    Interrupciones del servicio: Reglas demasiado restrictivas pueden bloquear tráfico legítimo, causando fallos en aplicaciones o servicios.
    Fuga de datos: Configuraciones incorrectas pueden permitir la exfiltración de datos sensibles.
 * Solución: Revisar y ajustar reglas de grupos de seguridad:
   Limitar las reglas de entrada (inbound) y salida (outbound) a solo las direcciones IP, puertos y protocolos necesarios.
   Evitar usar 0.0.0.0/0 a menos que sea estrictamente necesario.
   Revisar y ajustar ACLs: Las ACLs son stateless, por lo que se debe configurar reglas explícitas para el tráfico de entrada y salida. Asegúrarse de que las ACLs no bloqueen tráfico legítimo entre subredes o hacia Internet.
   ademas seria conveniente a manera de prevencion herramientas de monitoreo como VPC Flow Logs

* **Falta de aislamiento entre subredes:** 
  * descripcion: Las subredes dentro de una VPC no están adecuadamente aisladas entre sí, lo que permite que recursos en una subred accedan a recursos en otras subredes sin restricciones. Esto ocurre cuando no se configuran correctamente las tablas de rutas (Route Tables) o las listas de control de acceso (ACLs)
  * impacto: Riesgo de seguridad: Un atacante que comprometa un recurso en una subred podría moverse lateralmente y acceder a recursos en otras subredes.
	Fuga de datos: Información sensible almacenada en una subred podría ser accesible desde otras subredes no autorizadas.
  * solucion: Revisar y ajustar tablas de rutas: Asegúrarse de que cada subred tenga una tabla de rutas adecuada que controle el tráfico entre subredes.
    Limitar el tráfico entre subredes a solo lo necesario
    Usar NACLs para definir reglas de tráfico entre subredes, permitiendo solo el tráfico autorizado

* **Problemas de conectividad a internet**. 
 * descripcion: Los recursos dentro de una VPC no pueden conectarse a Internet o no pueden ser accesibles desde Internet. Esto ocurre debido a configuraciones incorrectas en componentes como Internet Gateway (IGW), tablas de rutas, NAT Gateway, grupos de seguridad o NACLs (Network Access Control Lists)
 * impacto: Interrupción de servicios:Los recursos que dependen de Internet (como servidores web o aplicaciones) no pueden funcionar correctamente.
   Inaccesibilidad desde Internet: Los usuarios externos no pueden acceder a servicios públicos alojados en la VPC. 
 * solucion: Asegúrarse de que un IGW esté asociado a la VPC.
   Verificar que las subredes públicas tengan una ruta en su tabla de rutas que apunte al IGW y Confirma que las subredes públicas tengan rutas correctas hacia el IGW.
   Asegúrarse de que los grupos de seguridad permitan el tráfico necesario (por ejemplo, HTTP/HTTPS para servidores web
   
 
   
   * ***Problemas de resolución de nombres DNS:**
   * descripcion: Los recursos dentro de una VPC no pueden resolver nombres de dominio (DNS) correctamente, lo que impide el acceso a servicios externos o internos. Esto ocurre debido a configuraciones incorrectas en el DNS de la VPC o grupos de seguridad.
   * impacto: Las aplicaciones que dependen de la resolución de nombres (como acceso a APIs externas o servicios de AWS) no pueden funcionar correctamente.
    Los recursos dentro de la VPC no pueden comunicarse entre sí usando nombres de dominio.
   * solucion: Asegúrarse de que la opción **"enableDnsSupport"** esté habilitada en la VPC. Esto permite que los recursos dentro de la VPC utilicen el DNS proporcionado por AWS.
    Asegúrarse de que la opción **"enableDnsHostnames"** esté habilitada si se desea que las instancias en la VPC reciban nombres de host DNS públicos

   *  **Routing incorrecto de paquetes**
   * descripcion. Los paquetes de red no se enrutan correctamente dentro de la VPC, lo que impide la comunicación entre recursos o con redes externas. Esto ocurre debido a configuraciones incorrectas en las tablas de rutas (Route Tables), VPC Peering, VPN, Direct Connect o NAT Gateway.
   *  impacto: Interrupción de servicios: Los recursos dentro de la VPC no pueden comunicarse entre sí o con redes externas, lo que afecta el funcionamiento de aplicaciones y servicios.
   Inaccesibilidad desde/hacia Internet: Los recursos en subredes públicas no pueden enviar o recibir tráfico desde Internet.
   * solucion: s se estás usando una VPN o Direct Connect, se verifica que las rutas estén correctamente propagadas a las tablas de rutas de la VPC.
    Si los recursos en subredes privadas necesitan acceso saliente a Internet, configura un NAT Gateway en una subred pública y agrega una ruta en la tabla de rutas de la subred privada
  
