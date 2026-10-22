Parte A · Hecha en Entregable 5

Parte B · Preparar un entorno controlado (CE d)

| Medida de aislamiento | ¿Hecho? | ¿Qué riesgo evita? |
| --------------------- | ------- | ------------------ |
| Sin carpetas compartidas ni portapapeles | Si | Información que pueda sacar el malware. |
| Snapshot previo | Si | Si algo sale mal, se puede volver a la maquina tal y como estava. |
| Máquina que no contiene datos personales ni credenciales | Si | Tus datos pueden llegar a caer en malas manos. |

Parte C · El fichero EICAR: una amenaza de mentira (CE e)

En mi caso lo detectan 6 motores
<img width="592" height="157" alt="image" src="https://github.com/user-attachments/assets/3a3cf746-e14a-4ed9-b94d-b4a3f7850288" />

Parte D · Instalar y usar ClamAV (CE e)

<img width="438" height="31" alt="image" src="https://github.com/user-attachments/assets/9bc43b5d-082d-4e02-857f-7b29065fb318" />

<img width="740" height="370" alt="image" src="https://github.com/user-attachments/assets/ca8b7ea6-7639-4c3b-bc62-a275a9127bab" />

Pregunta D: ¿Por qué suele ser mejor mover a cuarentena que borrar directamente? ¿Qué pasaría si ClamAV marcara por error un fichero importante del ERP de Torrent?

Es mejor moverlo por si el antivirus comete un error(falso positivo) con un archivo crítico del ERP, puede llegar a romper el programa de la empresa.

D6. Detectar rootkits
<img width="813" height="172" alt="image" src="https://github.com/user-attachments/assets/73fe6c00-fd6a-4f86-8661-1765f7f0c7b9" />

Parte E · Análisis estático: mirar sin ejecutar (CE d)

<img width="812" height="417" alt="image" src="https://github.com/user-attachments/assets/1be3e410-1d4c-4b34-afce-243ae6abbe2a" />

¿Qué crees que hace cada línea?

La primera te crea un archivo dir, despues copia algo, y ya las ultimas no tengo nidea.

¿Crea ficheros?

Si

¿Abre puertos?

Si

¿Modifica algo para sobrevivir a un reinicio?

Si por que copia en otras carpetas

Si fuera un .exe binario, ¿qué habría que hacer en su lugar?

Si fuera un .exe binario no podriamos usar cat, solo aparecerian símbolos que nosotros no entendemos.

Parte F · Análisis dinámico: observar qué hace (CE d)


| Qué hace | Evidencia (comando y salida) | ¿Qué fase del ataque recuerda? |
| -------- | ---------------------------- | ------------------------------ |
| Crea ficheros o carpetas | Archivos nuevos identificados mediante `diff ~/antes_tmp.txt ~/despues_tmp.txt`. Salida: `> /tmp/.cache_sistema/actualizador.sh` | **Instalación y Acciones sobre Objetivos: Ocultación de herramientas y payloads en directorios de escritura pública (`/tmp`). |
| Abre algún puerto o proceso | Identificado mediante `diff ~/antes_puertos.txt ~/despues_puertos.txt`. Salida: Puerto `8081` en estado *LISTEN* levantado por `python3`. | **Mando y Control (C2) / Explotación: Apertura de una puerta trasera local para el acceso a la información expuesta. |
| Intenta persistir | Detectado mediante `diff ~/antes_cron.txt ~/despues_cron.txt`. Salida: `> @reboot /bin/bash /tmp/.cache_sistema/actualizador.sh` | Persistencia: Mecanismo para asegurar la ejecución automática del código malicioso tras reiniciar el servidor afectado. |

Comprobad la persistencia:
Si, vuelve a aparecer.

Erradicación:
<img width="607" height="92" alt="image" src="https://github.com/user-attachments/assets/4114538d-5777-49d8-a0b1-58f2873d7323" />

Pregunta F: Habéis encontrado el comportamiento comparando "antes" y "después". ¿Cuál es el equivalente en un servidor real de Torrent si nadie hizo la foto inicial? ¿Qué relación tiene con el inventario de servicios que hicisteis en la práctica anterior?

En un servidor de producción real seria inviable tener una "foto limpia" antes de la infección, esto es la comparativa a una (Security Baseline) gestionada con herramientas de Auditória.

La relación con el inventario de servicios de la práctica anterior es total: el inventario actúa como la lista oficial de "lo que se conoce y es legal" en la empresa. Al tener ese inventario saltará de inmediato en los sistemas de monitorización como una anomalía, haciendo asi que se detecte fácil.

Parte G · Preventivo o paliativo (CE c, e)

| Medida | Preventiva | Paliativa |
| ------ | ---------- | --------- |
| Mantener el sistema actualizado | X | |
| ClamAV escaneando a demanda un disco | | X |
| Descargar software solo de repositorios oficiales | X | |
| Copia de seguridad semanal desconectada de la red | | X |
| Cuenta de usuario sin privilegios de administrador | X | |
| rkhunter tras sospechar una intrusión | | X |
| Formación del personal contra el phishing | X | |

