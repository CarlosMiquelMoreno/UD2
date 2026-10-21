# Laboratorio fases 1 y 2 — Estudio Torrent

## A1. whois y nslookup
No es necesario (realizado en clase bajo escenario ficticio).

## B. Antes y después

### 1. Inventario de servicios inicial (Contramedida 1)
Basándonos en la suposición de trabajo de que este servidor solo debe ofrecer servicio web (puerto 80) y administración remota SSH (puerto 22), se realizó el inventario de puertos mediante `sudo netstat -tulpn` y se determinó el plan de acción:

| Puerto | Servicio (Nombre) | ¿Es necesario? | Decisión |
| ------ | ----------------- | -------------- | -------- |
| **21** | FTP (vsftpd) | No | Apagar / Desactivar |
| **22** | SSH | Sí | Mantener abierto |
| **23** | Telnet | No | Apagar / Desactivar |
| **25** | SMTP (Correo) | No | Apagar / Desactivar |
| **80** | HTTP (Web) | Sí | **Mantener abierto |
| **512** | Rexec / Rlogin | No | Apagar / Desactivar |

### 2. Contramedidas aplicadas
Para securizar el servidor bajo el principio de mínimo privilegio, se ejecutaron las siguientes acciones en **Torrent-Vulnerable**:

*   **Apagado de servicios fijos y por demanda:**
    ```bash
    sudo /etc/init.d/vsftp stop
    sudo /etc/init.d/postfix stop
    sudo /etc/init.d/openbsd-inetd stop
    sudo /etc/init.d/xinetd stop
    ```
*   **Bloqueo de respuestas ICMP (Ping):**
    ```bash
    sudo iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
    ```
*   **Detección y registro de escaneos (Ampliación):**
    ```bash
    sudo iptables -I INPUT 1 -p tcp --syn -m limit --limit 5/second -j LOG --log-prefix "Posible-escaneo"
    ```

### 3. Tabla comparativa: Antes vs Después

| Aspecto | Antes | Contramedida aplicada | Después |
| ------- | ----- | --------------------- | ------- |
| **Puertos abiertos** | Múltiples puertos activos (21, 23, 25, 512, etc.) | Desactivación de `xinetd`, `inetd`, `vsftp` y `postfix`. | **Solo puertos 22 (SSH) y 80 (HTTP).** |
| **Servicios visibles** | Expuestos todos los servicios por defecto de Metasploitable. | Reducción de la superficie de exposición del sistema. | **Únicamente SSH y Servidor Web.** |
| **Respuesta al ping** | Responde activamente de forma normal. | Regla de iptables con acción `DROP`. | **No responde (100% de paquetes perdidos).** |

<img width="722" height="320" alt="Captura de pantalla 2026-10-21 105400" src="https://github.com/user-attachments/assets/f9c48b5b-76f3-406d-9f42-35f679ef5f2c" />



### B5. Preguntas finales

**1. ¿Qué contramedida ha reducido más lo que ve el atacante? ¿Por qué?**
La **Contramedida 1 (apagar servicios)**. Al detener procesos como inetd o vsftp, los puertos se cierran físicamente y desaparecen por completo. El bloqueo del ping solo oculta la máquina, pero apagar servicios elimina directamente los vectores de ataque.

**2. Si solo ocultáis un banner pero el servicio sigue activo, ¿la vulnerabilidad sigue ahí? Razonad la respuesta.**
**Sí.** Ocultar el banner dificulta que el atacante descubra la versión de forma automática (seguridad por oscuridad), pero si el servicio sigue ejecutándose en memoria, sigue siendo igual de vulnerable ante un exploit directo.

**3. Torrent-Vulnerable usa un sistema operativo sin soporte desde hace años. ¿Puede una contramedida de estas sustituir a actualizarlo? ¿Qué haríais en una empresa real?**
**No, nunca.** Las contramedidas mitigan el riesgo, pero no solucionan los fallos de seguridad internos del sistema operativo o del kernel. En una empresa real, la prioridad es **actualizar o migrar** el sistema; si no se puede por software heredado, se aísla por completo en una red privada (VLAN).

**4. De todas las contramedidas de las partes A y B, ¿cuáles evitan que el atacante encuentre información y cuáles solo ayudan a detectar que lo están intentando?**
* **Evitan información (Prevención):** Apagar servicios innecesarios, bloquear el ping (DROP) y ocultar banners.
* **Detectan el intento (Detección):** La regla de registro de iptables (LOG con "Posible-escaneo"), que no frena el ataque pero avisa en los logs (dmesg).

