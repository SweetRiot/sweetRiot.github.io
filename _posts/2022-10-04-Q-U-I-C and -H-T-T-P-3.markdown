Instale Wireshark nuevamente.


Empecé a filtrar mis paquetes por https usando `tls` y luego por la ip de destino con `ip.dst==173.194.161.8`, me dio curiosidad esa IP porque estaba usando el protocolo UDP, supuse que esa IP sería de Youtube/Google ya que tenía de fondo un vídeo de Youtube y para el streaming se usa UDP por ser más rápido. Pero me entró la duda. 


¿Acaso UDP no es solo para streaming en vivo ? Porque ese protocolo no asegura la integridad del envío y puede haber pérdida de información. Yo estaba viendo los vídeos 'on demand' y no en vivo. Entonces ¿ por qué Youtube está usando el protocolo UDP ? 


Me puse a ver qué otros protocolos estaba usando 173.194.161.8 con `ip.dst==173.194.161.8` y habían varios paquetes con el protocolo QUIC.


Resulta que QUIC es un protocolo de la capa de transporte que se construye usando UDP, pero con la capacidad de asegurar la integridad y la seguridad de los archivos. ¿Como TCP?


Al parecer sí, como TCP, pero mejor, porque es más rápido(casi siempre).


Al parecer, tan bueno es QUIC que HTTP/3 a diferencia de HTTP/1 Y HTTP/2 dejará de usar TCP, para usar netamente QUIC que está basado en UDP.


Estuve averiguando sobre cómo implementar QUIC en mis servicios web, por suerte no tengo que cambiar el código de mi aplicación, ya que puedo usar NGINX para enviar vídeos usando QUIC y conectarme con mis clientes usando HTTP/3.



Seguiré explorando QUIC y HTTP/3.

