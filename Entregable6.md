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
<img width="802" height="242" alt="image" src="https://github.com/user-attachments/assets/1a39958b-cff9-4ca2-a6dd-4a51a16e6d3c" />

B4. Buscad paquetes instalados que no proceden de ningún repositorio (instalados a mano):
<img width="807" height="175" alt="image" src="https://github.com/user-attachments/assets/e2e66011-e136-4dd0-bdd0-6c209b4c35ee" />

B5. Comprobad si algún fichero de un paquete ha cambiado desde que se instaló:
<img width="585" height="177" alt="Captura de pantalla 2026-10-22 105620" src="https://github.com/user-attachments/assets/bc8ae6ee-be86-4054-9e26-3f7bdd27eddf" />

Pregunta B: dpkg -V ¿detectaría un rootkit que además hubiera modificado la base de datos de dpkg?

No lo detectaría porque el comando dpkg -v funciona para comparar archivos actuales del sistema contra la información de control que esta en la base d edatos local de dpkg.

¿Por qué conviene comparar con una copia guardada fuera del sistema?

Conviene por que dicho en la fase 4 lo que quiere hacer el atacante es pasar desapercibido eliminando todas las evidencias de su acceso.

Parte C · Verificar una descarga: hash y firma

C1. Descarga:

mkdir -p ~/verif && cd ~/verif
wget https://ftp.gnu.org/gnu/hello/hello-2.12.1.tar.gz
wget https://ftp.gnu.org/gnu/hello/hello-2.12.1.tar.gz.sig
wget https://ftp.gnu.org/gnu/gnu-keyring.gpg

C2. Calculad el hash:

<img width="807" height="45" alt="image" src="https://github.com/user-attachments/assets/33d24350-8265-49a1-bf63-b39a69b0fc18" />

C3. Verificad la firma usando la lista de claves de GNU:

<img width="772" height="180" alt="Captura de pantalla 2026-10-22 161651" src="https://github.com/user-attachments/assets/d3c93ddd-4c6a-4415-8d07-c43617ae87aa" />
Esta es la firma que nos ha dado.

C4. El experimento: ¿qué pasa si alguien toca el fichero? Haced una copia y añadid un carácter:

<img width="810" height="92" alt="image" src="https://github.com/user-attachments/assets/09ee6c2b-fdd8-4428-85dc-b820571ce75d" />
Al haber cambiado, sabe que no es la que se utilizó antes.

C5. Pregunta C: completad:

| Situación | ¿Basta con el hash? | ¿Hace falta la firma? ¿Por qué? |
| --------- | ------------------- | ------------------------------- |
| El fichero se corrompió al descargarlo | Si | No, con que el archivo se corrompa, el hash ya cambia. |
| Un atacante cambió el fichero y el hash publicado en la misma web | No | Si, ya que si cambia el hash el atacante y lo pone para que le de el ok. |
| Descargas desde un espejo (mirror) que no es de confianza | No | Si, al no ser de confianza el hash puede estar alterado para que pase desapercibido. |

Parte D · Política de actualizaciones para Torrent

La política de seguridad sería así.
- Cada mes 1 socio se encargara de aplicar las actualizaciones de seguridad cada fin de semana.
- Los parches del ERP y el servidor de impresión se probaran en entornos aislados antes de ponerlos.
- Las actualizaciones automáticas no se utilizaran para evitar las caídas inecesarias del servidor.
- Solo se instalara software de repositorios oficiales y tiene que ser autorizado por los 3 socios.
- Todo equipo que haya superado su (EOL) se cambiara en un máximo de 30 días.
