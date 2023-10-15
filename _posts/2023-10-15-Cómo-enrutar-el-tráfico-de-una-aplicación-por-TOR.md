Si quiero tener una navegación anónima por la web puedo usar en navegador Tor, esto me mantendrá anónimo cuando visite cualquier página web. 
Si quiero que una app de escritorio diriga todo su tráfico primero por la red Tor, se puede buscar en las configuraciones y ver si me permite asignar un Proxy. 
Pero ¿ qué pasa con las app que no me permiten esta configuración ? ¿Cómo puedo anonimizar mi tráfico? 
Podemos usar la herramienta del proyecto Tor, llamada Torsocks, que está disponible para el sistema operativo de Linux.
La instalación desde Ubuntu es muy sencilla, solo tienes que ejecutar el siguiente comando 
sudo apt install torsocks
Para usar esta herramienta solo tienes que ejecutar el siguiente comando en la terminal: 
torsocks nombre_de_la_aplicación
esto hará que todo el tráfico de mi aplicación elegida vaya por la red Tor, no hay forma que el tráfico de mi aplicación vaya por fuera de la red Tor, ya que a cualquier intento Torsocks cerrará la aplicación. 

Un experimento que hice para probar el funcionamiento de Torsocks fue usar la aplicacion Wget de Linux, que basicamente realizar un petición http a una web.
La web que usaré será https://www.getip.org/

En la terminal poner
torsocks wget https://www.getip.org/
wget realizará una petición a dicha web y esta web me devolverá la IP de la que cree que me estoy conectando. 
Obtengo la respuesta por medio de un archivo html, que se almacena en mi directorio desde donde ejecuté wget.
Puedes abrir el archivo index.html con un navegador y así ver la IP, pero como estoy en Ubuntu server, simplemente usaré la herramienta "cat" que me sirve para leer archivos de texto desde la terminal. 
entonces ejecuto lo siguiente: 
cat index.html, en la misma terminal puedo observar la IP que me devuelve, el cuál es en este caso una IP de Wisconsin - Estados Unidos.
Quedando en evidencia así que la herramienta Torsocks ha redirigido mi tráfico de manera exitosa.  