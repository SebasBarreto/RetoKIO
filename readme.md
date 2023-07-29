Tarea Semana 2 - Ethical Hacking: Reto KIO
Introducción

Este informe documenta el análisis de vulnerabilidades, la explotación, la escalación de privilegios y la obtención de banderas en la máquina objetivo KIO. El reto se enfocó en identificar debilidades en servicios, aprovechar exploits y demostrar habilidades prácticas en ciberseguridad.
Paso 1: Reconocimiento

    Identificación de la máquina objetivo:
        Herramientas utilizadas:
            ifconfig: Para identificar la IP de la máquina atacante (Kali).
            arp-scan -l: Para listar dispositivos en la red.
        Resultado:
            Dirección IP de KIO: 192.168.198.131
            MAC Address: 00:0C:29:9B:0C:22

    Escaneo de puertos:
        Comando:

        nmap -sS -p 1-65535 192.168.198.131

        Puertos abiertos:
            22/tcp (SSH)
            80/tcp (HTTP)
            111/tcp (rpcbind)
            139/tcp (netbios-ssn)
            443/tcp (HTTPS)
            1024/tcp (KDM)
        Sistema operativo identificado: Linux 2.4.x

Paso 2: Análisis de Vulnerabilidades

    Enumeración de servicios:
        Herramientas utilizadas:
            Dirbuster: Para listar posibles archivos y directorios en el servicio HTTP.
            Nikto: Para identificar versiones de Apache y OpenSSL.
            Enum4linux: Para enumerar usuarios, grupos y archivos compartidos en Samba.

    Identificación de vulnerabilidades:
        Versión de Samba detectada: 2.2
        Uso de Metasploit:
            Configuración del objetivo con:

            set RHOSTS 192.168.198.131

            Ejecución de exploits específicos para Samba.

Paso 3: Explotación

    Ataque inicial:
        Intento de explotación en el puerto 22 (OpenSSH) para un RCE (Ejecución Remota de Comandos), sin éxito.

    Explotación exitosa:
        Uso de Metasploit con el payload:

        set payload linux/x86/shell_reverse_tcp

        Ejecución del exploit y obtención de un reverse shell:
            Resultado: Acceso root confirmado mediante el comando bash -i.

Paso 4: Escalación de Privilegios

    Uso de Metasploit y el payload linux/x86/shell_reverse_tcp.
    Logro: Acceso completo como usuario root en la máquina KIO.

Paso 5: Obtención de las Banderas

    Comando utilizado:

    find / -name bandera*.txt 2>/dev/null

        Banderas encontradas y su contenido:
            Bandera 1: /home/john/bandera1.txt
            684d0624c19cac22a44a8413795368b9
            Bandera 2: /root/bandera2.txt
            c9b2db2dbe3d8e65485c6c348785a760
            Bandera 3: /home/harold/bandera3.txt
            9699a2a93f0d7eeb172dca2de51d3db2

Herramientas Utilizadas

    Reconocimiento:
        ifconfig, arp-scan, ping, nmap.
    Análisis:
        Dirbuster, Nikto, Enum4linux.
    Explotación:
        Metasploit, searchsploit.
    Otras:
        find, cat.

Conclusiones

    Éxitos:
        Se logró acceso como usuario root mediante la explotación de una vulnerabilidad en Samba.
        Identificación y obtención de las tres banderas.
    Lecciones aprendidas:
        La importancia de aplicar parches de seguridad y restringir permisos en servicios críticos.
        La necesidad de monitorear y detectar actividades inusuales en tiempo real.

Recomendaciones

    Mitigación de vulnerabilidades:
        Actualizar Samba a una versión segura.
        Configurar permisos adecuados en archivos y directorios.
    Prácticas de seguridad:
        Realizar auditorías periódicas y simulaciones de pruebas de penetración.
        Implementar monitoreo continuo para identificar ataques en tiempo real.