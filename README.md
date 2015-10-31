# Obtención del certificado gratis de startssl.com

Pasos a seguir para la obtención del certificado:

Entrar en startssl.com e ir a 'Control Panel':

1. Seleccionamos 'Express Lane'.
![alt tag](images/1.png?raw_true "Entrar en Control Panel")

2. Rellenamos el formulario con los datos personales, es recomendable no usar datos falsos.
![alt tag](images/2.png?raw_true "Rellenar formulario")

3. Después de rellenar el formulario, nos envían un correo con un código de validación, hay que ponerlo para poder continuar.
![alt tag](images/3.png?raw_true "Confirmar con el código recibido")

4. Generamos la clave privada del certificado personal.
![alt tag](images/4.png?raw_true "Generar clave privada")

5. Instalamos el certificado en el navegador, será necesario para poder administrar nuestro dominio en startssl.com posteriormente.
![alt tag](images/5.png?raw_true "Instalar certificado")

6. Verificamos que el certificado se instaló corretamente en el navegador.
![alt tag](images/5.1.png?raw_true "Verificar certificado")

7. Felicidades! Tu certificado personal se ha instalado en el navegador. (Más abajo explico cómo exportarlo para guardarlo y usarlo en otros pcs o navegadores)
![alt tag](images/6.png?raw_true "Continuar")

8. Ahora sí ponemos el nombre del dominio para el que queremos el certificado.
![alt tag](images/7.png?raw_true "Poner nombre del dominio")

9. Elegimos la cuenta de correo donde queremos que nos manden la verificación del certificado del dominio.
En el caso del dominio de h¡hostinger.es, previamente hemos tenido que crear una cuenta de correo en nuestro servidor de correo gratuito con uno de estos nombres: postmaster, hostmaster, webmaster.
![alt tag](images/8.png?raw_true "Elegir cuenta de correo del dominio")

10. Ponemos el código que nos envíen a la cuenta de administrador del dominio.
![alt tag](images/9.png?raw_true "Escribir código de activación el el fromulario")

11. Generar la clave privada del dominio. Ojo! guardar muy bien el password que pongamos, si lo perdemos no podremos descifrar la clave del dominio.
![alt tag](images/10.png?raw_true "Generar clave privada del dominio")

12. Copiar, sin formato, la clave y guardarla en un fichero de texto plano, por ejemplo, 'ssl_crypted.key'
![alt tag](images/11.png?raw_true "Copiar y guardar clave cifrada")

13. Descifrar la clave descifrada con openssl en la terminal y guardarla en un fichero, por ejemplo, 'ssl.key'. Guardar ese fichero en lugar seguro y solo accesible por nosotros.
![alt tag](images/12.png?raw_true "Descifrar y guardar clave en un fichero.")

14. Ahora crear el certificado para nuestro host. Elegir el dominio donde se encuentra el host.
![alt tag](images/13.png?raw_true "Elegir el dominio")

15. Escribir el nombre del host.
![alt tag](images/14.png?raw_true "Escribir nombre del host")

16. Esperar 3 horas aproximadamente a que verifiquen nuestros datos.
![alt tag](images/15.png?raw_true "Esperar pacientemente")

17. Mientras esperamos podemos ir exportando y guardando en lugar seguro nuestro certificado personal. Elegimos el certificado en cuestión y pulsamos en 'exportar'
![alt tag](images/16.png?raw_true "Seleccionar certificado personal y exportarlo")

18. Le ponemos un password a nuestro certificado personal. Ojo! Si perdemos el password ya no podremos acceder a nuestra cuenta de startssl.com en caso de borrar el navegador en el que lo tenemos instalado,
![alt tag](images/16.1.png?raw_true "Poner contraseña al certificado.")

19. Una vez nos avisen por correo que ya tenemos nuestro certificado listo, volvemos a entrar en 'Control Panel' y pulsamos en 'Authenticate' para entrar en nuestra cuenta de startssl.com
![alt tag](images/17.png?raw_true "Authenticate")

20. En caso de ser dueños de varios dominios y tener varios certificados, elegir el certificado del dominio en cuestión.
![alt tag](images/17.1.png?raw_true "Elegir certificado")

21. Pulsar en 'Retrieve Certificate' para poder descargar el certificado y elegir el único que debemos tener.
![alt tag](images/18.png?raw_true "Descargar certificado")

22. Copiar y guardar el certificado en un fichero '.crt'. Guardar en lugar seguro.
![alt tag](images/19.png?raw_true "Guardar certificado")

23. Comprobar que el fichero '.crt' contiene todos nuestros datos y el nombre del host.
![alt tag](images/19.1.png?raw_true "Guardar certificado")

24. Último paso. Si queremos usar nuestro certificado para un servidor web con una página en https, descargar el fichero '.pem' necesario de la página de startssl.com, ' http://www.startssl.com/certs/sub.class1.server.ca.pem '

# Resumen

Con los 3 ficheros tenemos todo lo necesario para montar un servidor web en https, y con un certificado que todos los navegadores aceptan sin necesidad de instalar nada por parte del usuario que acceda:
- ssl.key   (descifrado)
- fichero.crt (del host)
- sub.class1.server.ca.pem

Evidentemente todo esto lo podemos hacer autofirmando nosotros mismo un certificado y creando una entidad certificadora, pero de esta forma se hace en condiciones y no cuesta ningun trabajo ni dinero.

# NUEVOS CERTIFICADOS PARA MÁS HOSTS

En caso de tener varios hosts, y que le queramos sacar certificados, en principio no se puede, pero podemos hacer lo siguiente:

1. Crear .csr y .pem en el host en cuestión mediante este comando:
	openssl req -newkey rsa:2048 -nodes -keyout subdominio.ejemplo.com.pem -sha256 -out subdominio.ejemplo.com.csr

2. Proteger el .pem:
	chmod 600 subdominio.ejemplo.com.pem

3. Copiar el texto del .csr y ponerlo en el formulario de startssl.com

4. Elegir el dominio que tenemos registrado, y poner el subdominio

5. Descargar el el certificado y pegar el contenido en un fichero .crt

Ya tenemos el '.crt' necesario para nuestro subdominio.

