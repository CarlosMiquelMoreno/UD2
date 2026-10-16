Parte B · ¿De dónde vienen los programas instalados?

B1
Investiga el fichero donde están configurados los repositorios y 
comenta el significado de cada una de las líneas y su contenido.
Types: Aqui indica que los paquetes son binarios ya compilados.
URIs: Dirección del servidor donde se descargan los archivos.
Suites: Define las ramas de software que se van a consultar.
Components: Son las categorias de software según la licencia de la versión.
Signed-By: La ruta local a la clave criptográfica GPG.

B2
Reflexiona: ¿qué pasaría si un atacante introduce una clave falsa en /usr/share/keyrings/? 
¿y si intercepta o reemplaza la clave oficial de Ubuntu ubuntu-archive-keyrings.gpg?
Si alguien pone una clave falsa en la ruta, podría llegar a firmar metadatos malos que APT piensa que son buenos.
Podría afectar la verificación de autenticidad de todos los repositorios.
