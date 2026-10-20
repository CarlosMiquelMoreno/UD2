Parte A · ¿Está actualizado el sistema?

A1. Anotad qué versión de sistema operativo y kernel tenéis:

SO Ubuntu 24.04.3 LTS

Kernel 7.0.0-31-generic

A2. Pedid al sistema la lista de paquetes disponibles y qué se puede actualizar:

*Comprobaciones dentro del sistema*

Hay casi 200 paquetes con actualización pendiente.

A3. Simulad la actualización sin aplicarla:

*Simulacion hecha*

A4. ¿Y si el sistema ya no recibe parches? Buscad en https://endoflife.date la fecha de fin de soporte de:
| Sistema | Fecha de fin de soporte | ¿Recibe parches hoy? |
| ------- | ----------------------- | -------------------- |
| Torrent-Auditor | Mediados 2029 | Si |
| Torrent-Vulnerable | Mediados 2013 | No |

Pregunta A: En la oferta de empleo de Torrent (dossier de la UD02) decían que trabajaban con "Ubuntu 8.04". Aunque pusieran todas las contraseñas bien, ¿qué problema sigue sin tener solución?

Tendría aun muchos problemas ya que al ser una versión antigua ya se sabe todo de ella, con la seguridad puesta y todo, se puede acceder a las bibliotecas de exploits públicos para mirarlo.

Parte B · ¿De dónde vienen los programas instalados?

B1. Mirad de qué repositorios se descarga vuestro sistema:
Investiga el fichero donde están configurados los repositorios y 
comenta el significado de cada una de las líneas y su contenido.
Types: Aqui indica que los paquetes son binarios ya compilados.
URIs: Dirección del servidor donde se descargan los archivos.
Suites: Define las ramas de software que se van a consultar.
Components: Son las categorias de software según la licencia de la versión.
Signed-By: La ruta local a la clave criptográfica GPG.

B2. apt solo instala paquetes firmados por claves en las que confía. Mirad dónde están esas claves:
Reflexiona: ¿qué pasaría si un atacante introduce una clave falsa en /usr/share/keyrings/? 
¿y si intercepta o reemplaza la clave oficial de Ubuntu ubuntu-archive-keyrings.gpg?
Si alguien pone una clave falsa en la ruta, podría llegar a firmar metadatos malos que APT piensa que son buenos.
Podría afectar la verificación de autenticidad de todos los repositorios.

B3. Información de un paquete concreto. Elegid openssh-server o curl:
