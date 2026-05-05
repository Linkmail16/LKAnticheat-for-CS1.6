# LK Anticheat — CS 1.6

Anticheat para Counter-Strike 1.6 compuesto por un ejecutable lanzador, un módulo cliente y un plugin de servidor AMX Mod X.

---

## Archivos

| Archivo | Descripción |
|---|---|
| `LKAnticheat.exe` | Lanzador. Se mantiene abierto mientras juegas |
| `LKHook.dll` | Módulo de protección inyectado en el cliente |
| `lk_anticheat.amxx` | Plugin compilado para el servidor AMX Mod X |

---

## Instalación

### Cliente

1. Abre **LKAnticheat.exe** antes o después de entrar al servidor.
2. El lanzador descarga automáticamente el módulo si no lo encuentra, lo verifica y lo inyecta en el juego.
3. Déjalo abierto mientras juegas. Puedes minimizarlo a la bandeja del sistema.

> La primera vez que lo abras creará un acceso directo en el escritorio.

### Servidor

1. Copia `lk_anticheat.amxx` en `cstrike/addons/amxmodx/plugins/`.
2. Añade `lk_anticheat.amxx` a `plugins.ini`.
3. Reinicia el servidor.

---

## Qué hace

**LKAnticheat.exe** actúa como lanzador y gestor. Detecta cuando se abre CS 1.6, descarga y verifica el módulo de protección, y lo inyecta en el proceso del juego. Mantiene el módulo actualizado comparando versiones con el servidor antes de cada sesión.

**LKHook.dll** se ejecuta dentro del proceso del juego y realiza análisis continuos en tiempo real. Detecta y cierra el juego ante la presencia de software no autorizado o modificaciones en la sesión activa. Se comunica con el servidor a través del plugin para reportar el estado del cliente.

**lk_anticheat.amxx** gestiona la verificación de cada jugador al conectarse. Los jugadores sin el módulo activo o que no superen la verificación son expulsados automáticamente. Los administradores disponen de comandos para consultar el estado y lanzar análisis manuales.

---

## Comandos de administrador

Requieren flag `ADMIN_KICK` (`d`).

| Comando | Descripción |
|---|---|
| `lkac_check <jugador>` | Muestra el estado del anticheat de un jugador |
| `lkac_ping <jugador>` | Comprueba si el módulo responde |
| `lkac_scancommands <jugador>` | Lanza un análisis manual |

---

## Motivos de expulsión

| Mensaje | Causa |
|---|---|
| `LK Anticheat: no detectado` | El módulo no está activo o fue bloqueado |
| `LK Anticheat: verificacion fallida` | La verificación de autenticidad no pasó |
| `LK Anticheat: modulo no autorizado` | Se detectó software externo inyectado |
| `LK Anticheat: modulo oculto detectado` | Se detectó código oculto en memoria |
| `LK Anticheat: herramienta no autorizada` | Se detectó una herramienta de cheat activa |
| `LK Anticheat: modificacion de memoria` | Se detectó alteración del código del juego |
| `LK Anticheat: hack detectado` | Se detectaron comandos de hack registrados |
| `LK Anticheat: sin respuesta` | El módulo dejó de responder durante la sesión |

---

## Requisitos

- Windows 10 / 11 (x64)
- Counter-Strike 1.6 (Steam o no-Steam)
- Servidor con AMX Mod X 1.8.2 o superior

---

## Notas

- No requiere instalación de Visual C++ Redistributable.
- Compatible con múltiples instancias de CS abiertas simultáneamente.
- El módulo se descarga y verifica automáticamente en cada inicio; no es necesario actualizarlo manualmente.
