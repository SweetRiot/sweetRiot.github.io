Estuve realizando una página web sencilla, que permita al personal de un hotel registrar las habitaciones ocupadas y al dueño revisar esta información y ver estadísticas de sus habitaciones e ingresos. 


La aplicación la desarrollé usando NodeJS, Express como Framework, Passport.js para la autenticación y entre otras que usé para hashear las contraseñas o administrar los logs. 


De base de datos en un inicio usé MySQL, pero luego hice el cambio a SQLite, ya que esta aplicación hará un uso muy pequeño de la base de datos y por lo tanto no necesito una herramienta tan potente como MySQL. 


Luego de sortear todos los problemas y bugs que aparecieron en el desarrollo de la app, llegó el momento de poner el código en producción. 


En este momento evalué si debería usar plataforma como servicio, infraestructura como servicio.


Decidí al final trabajar con una infraestructura como servicio usando EC2 de AWS. Ya que tiene una capa gratuita y funcionalidades interesantes. En ella instalé Ubuntu Server como SO y luego NodeJS con NVM.
El código de mi aplicación está en un repositorio de Github, por lo tanto desde el servidor de AWS solo tuve que hacer un `git clone`. 
Los archivos delicados no están en GitHub, ellos los pasé de mi laptop al servidor usando `scp` junto con mi llave .pem para establecer una conexión segura con el servidor.


Configuré también el grupo de seguridad de AWS para permitir las conexiones entrantes al server, abrí solo 3 puertos, el 22 para SSH, 80 para http y 443 para https. El puerto 80 se mantiene abierto solo por si algún cliente se conecta usando http, mi servidor web NGINX lo redirecciona al puerto 443 para poder establecer una conexión segura.


Hice la instalación de todas las dependencias de NodeJS con `npm install`


Mi aplicación no puede abrir el puerto 80 o 443 porque eso requiere privilegios elevados en el servidor(desde el puerto 1 al 1023), hay maneras de ejecutar la aplicación usando `sudo` pero no es aconsejable, ya que si mi aplicación tiene algún problema de seguridad quedaría más expuesto ya que está siendo ejecutada con root. 

Luego de investigar resulta que la mejor solución es usar un Proxy Server, como NGINX, este puede estar escuchando en el puerto 80 y 443 sin problemas.


Configuré NGINX para que las solicitudes entrantes a esos puertos sean redireccionadas al puerto 5000 que es donde mi aplicación estaba escuchando. 


Cabe resaltar que usé Let's Encrypt para generar mi certificado SSL gratuitamente y poder tener conexiones HTTPS con mis clientes. 


Entre mi cliente y mi servidor se crea una conexión HTTPS y de NGINX a mi servidor web en NodeJS una conexión http. 


Cabe resaltar también que AWS tiene un servicio AWS Budgets que permite enviarte alertas cuando excedas costos. Definí el monto de dinero que al excederse AWS me informará.


Hacer este proyecto fue interesante. Me permitió ver todo el flujo de trabajo desde recoger los requerimientos del funcionamiento de la página, la elección de la tecnología adecuada para el tamaño del proyecto, tener en cuenta la seguridad de la web desde el código, en la infraestructura y luego en el deployment. Por último los costos de poner en producción el código.








