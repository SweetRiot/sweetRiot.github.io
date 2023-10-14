El día de hoy estuve aprendiendo sobre NGINX. 

Había escuchado sobre NGINX hace años, pensé que era un servidor web que se usaban hace años y que había quedado en desuso.
Pero no, resulta ser que es una herramienta potente y que se usa hoy en día. 
Se usa principalmente como un balanceador de carga(load balancer) y como un proxy inverso. 
Esto quiere decir que en vez de que un cliente envie directamente un request a tu servidor web, llegará a NGINX, el cuál se encargá de 
redigir la solicitud al servidor asignado.

Para hacer mi prueba primero tuve que instalar NGINX. Estuve evaluando si instalarlo en Windows 11 o Linux(Ubuntu), por experiencias pasadas trabajar con servidores en Windows se me hace tedioso, así que preferí crear una máquina virtual en VMWare e instalar Ubuntu Server. 
Realicé todas las instalaciones necesarias siguiendo las guías que hay en internet. 

Lo otro que hice fue configurar mis hosts en Ubuntu, configurando el documento "hosts" que está en el directorio /etc/ de Ubuntu
De esa forma en vez de usar IPs asigné 3 dominios locales (app1.local, app2.local, app3.local)
Hice esto debido a que NGINX para redirigir una solicitud se fija en el dominio y el puerto al que el cliente está enviando la solicitud. 

Luego en sites-available cree los 3 archivos de configuración, donde especificaba el dominio y puerto de cada aplicación que tenía. 

Luego para que estos sitios estén disponibles se tiene que crear un enlace simbólico, que es como crear un acceso directo hacia estas configuraciones que cree en sites-available. 
Estos accesos directos o enlaces simbolicos como se llaman en Linux deben ir en sites-enable. 

Una vez puesto esto 
corrí los siguientes comandos en la terminal bash de Ubuntu. 
nginx -t para verificar que mis archivos de configuracion estén bien
Luego recagar las configuraciones al servicio de NGINX que ya estaba corriendo, usé "sudo systemctl reload nginx"
Con esto nginx ya podía servir mis aplicaciones a mis clientes. 

Cabe resaltar que mis aplicaciones diponibles las realicé en nodejs, fueron servidores web muy simples. 

Algunos problemas que tuve es que mi app3 no la alojé en el mismo servidor donde se ejecutaba NGINX, si no en mi máquina principal con Windows. Tuve que abrir el puerto 80 ya que mi app3 que era también un servidor web en Nodejs estaba escuchando en el puerto 80 y Windows lo estaba bloqueando. Luego de abrir el puerto no hubo problemas. 


Lo más alucinante de todo esto es que tuve 3 servidores web corriendo, 2 en Linux y 1 en Windows, en diferentes máquinas y NGINX me lo enviaba correctamente. Sin duda, seguiré experimentando con NGINX. 