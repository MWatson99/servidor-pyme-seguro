# Diario del proyecto

## 2026-09-29

**Objetivo:** completar la instalación de Ubuntu Server, que se había quedado atascada el día anterior.

**Qué hice:**
- Diagnostiqué que la instalación se quedaba colgada siempre en el mismo paquete (`linux-firmware-intel-wireless`, 112 MB) durante la descarga de actualizaciones.
- Cambié la configuración de red de la VM de **Adaptador puente** a **NAT**.
- Repetí la instalación completa desde cero con la nueva configuración de red.

**Problemas y solución:**
- Con Adaptador puente, VirtualBox intenta "clonar" la tarjeta de red física del host. Algunos drivers de Wi-Fi (como el de mi tarjeta Realtek) no gestionan bien ese modo, y la VM se queda sin salida real a internet aunque parezca conectada.
- Solución: cambiar a NAT, donde VirtualBox gestiona la salida a internet a través de la propia conexión del host, sin depender del driver Wi-Fi. Esto significa que, de momento, no podré acceder a la VM desde fuera (SSH, navegador) sin configurar antes un reenvío de puertos (*port forwarding*), que abordaré en el Bloque 1 cuando toque SSH.

**Qué aprendí:**
- La diferencia entre los modos de red de VirtualBox: NAT (la VM sale a internet a través del host, pero el host no puede entrar a la VM sin configurar puertos) frente a Adaptador puente (la VM se comporta como un equipo más de la red física, con su propia IP, pero depende de que el driver de red del host lo soporte bien).
- Cómo diagnosticar un problema de instalación mirando el log completo del instalador (`View full log`) en vez de asumir que "va lento".

**Decisión de seguridad:** ninguna nueva hoy; queda pendiente configurar el reenvío de puertos de forma restrictiva (solo el puerto de SSH) cuando lleguemos a esa parte, en vez de abrir puertos innecesarios.

**Pendiente:** terminar el arranque tras la instalación, entrar por primera vez a la VM y empezar el caso práctico de usuarios y permisos.

## 2026-09-28

**Objetivo:** montar la base del proyecto: repositorio en GitHub y máquina virtual con Ubuntu Server.

**Qué hice:**
- Creé el repositorio público `servidor-pyme-seguro` y lo cloné con Git.
- Añadí la estructura de carpetas por bloques y un `.gitignore` que evita subir claves y contraseñas.
- Creé la VM `servidor-pyme` en VirtualBox (2 GB de RAM, 2 CPU, disco de 25 GB, red en adaptador puente).
- Empecé a instalar Ubuntu Server 24.04 con OpenSSH.

**Problemas y solución:**
- `Move-Item` falló porque PowerShell estaba dentro de la carpeta que quería mover. Solución: salir con `cd` y mover desde fuera.
- El instalador no dejó usar `admin` como usuario porque está reservado por el sistema.
- `DIARIO.md` se subió vacío a GitHub porque no se había guardado el contenido. Solución: comprobar el tamaño con `dir` antes de hacer commit.

**Qué aprendí:**
- Qué es clonar, hacer commit y push.
- El instalador usa LVM y deja espacio sin asignar por defecto.
- Conviene verificar el contenido de un archivo antes de subirlo.

**Decisión de seguridad:**
- `.gitignore` con reglas para claves y `.env` desde el primer commit, para no filtrar secretos.

**Pendiente:** terminar la instalación, entrar a la VM y hacer el caso de usuarios y permisos.
