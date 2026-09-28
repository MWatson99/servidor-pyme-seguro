# Diario del proyecto

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
