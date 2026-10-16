| Dato encontrado | Fuente (1-6) | ¿Para qué le sirve al atacante? | Contramedida propuesta |
| --------------- | ------------ | ------------------------------- | ---------------------- |
| SO del servidor sin soporte | 2 | Pueden por buscar vulnerabilidades sabiendo su versión y que además es antiguo. | Tener un sistema operativo con una versión mas actual. |
| SOs de los puestos antiguos | 2 | Un Windows 7 esta descatalogado, aparte de acarrear con algunos fallos. | Actualizar los sistemas operativos para tambíen un mejor seguridad de base. |
| Protocolos sin seguridad | 2 | vsftpd y FTP son protocolos con apenas seguridad, ya que pueden interceptar los datos muy fácil. | Utilizar otros como SFTP. |
| Falta de personal para ciberseguridad | 2 | No tener a alguien que se encargue de tu seguridad, significa que tendrás cosas abiertas que no sabras cerrar. | Contratar a alguien que te administre toda la seguridad de la empresa. |
| Uso del portátil como servidor | 2 | Respaldado con los dias que estan de vacaciones, puede robar ese portátil y hacerse con la información del servidor. | Comprar un servidor empotrado en vez de utilizar pórtatil. |
| Configuración de DNS insegura | 4 | Pueden empezar a hacerte phising o mandar malware para que google te quite el dominio. | Añadir DKIM, DMARC y cambiar el +all a -all. |
| Exposición de NAS y Pruebas | 4 | Tener expuestos los subdominios con IP publica se convierte en una entrada perfecta para que te roben información. | No mostrar al público las IPs que utilizas. |
| Contraseñas legibles | 5 | Saber cuales son tus contraseñas, con lo que pueden entrar haciendose pasar por ti | No tenerlas a la visto o mejor que te las genere un generador de contraseñas. |
| Conexión con redes públicas | 5 | Meterme en la misma red implica saber que puede hacer con alguna app de tráfico. | No utilizar redes públicas. |
| Datos sensibles al público | 6 | Datos como el número de otro socio, funciones de pago y el cuando no están en la empresa, puede llegar a ser útil al atacante para sobornar con esos datos | No mostrar esa información. |

Plan de ataque: Primero empezaría con una fase de investigación buscando exploits conocidos en los 2 sistemas operativos,
ubuntu 8.04 y windows y pondría un dominio muy parecido al de la empresa ya que el SPF es +all asi que me aceptaria sin problemas.
Desde ahi podria empezar a atacar como mandando un correo con un troyano desde un correo falso, cuando tenga acceso a uno de los
dispositivos puedo empezar a extraer toda información que pueda gracias a las contraseñas apuntadas y para acabar, descargo todo,
lo cifro, y pido un rescate.

Las mas importantes yo creo que serian:
- Exposición de NAS y PRUEBAS
- Configuración de DNS insegura
- SO del servidor sin soporte

 Eligiría estas por que son las que comprometen o dejan mas espacios para que los atacantes y por que las otras no, si aseguras las 3
 mas importantes, cierras todas las vulnerabilidades externas, con lo que ya no pueden entrar.
