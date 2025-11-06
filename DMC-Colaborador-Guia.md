# 📚 Guía para Colaborador DMC

**Proyecto:** DMC - denmicabez.online  
**Dominio:** [denmicabez.online](https://denmicabez.online)  
**Puerto VPS:** 11000  
**Chat ID Telegram:** _[Pendiente - solicitar al administrador]_

---

## 🎯 Objetivo del Proyecto

DMC es un proyecto independiente que opera de manera autónoma en la infraestructura compartida VPS. Tu rol como colaborador es supervisar, mantener y optimizar el sistema sin intervención manual constante.

---

## 🛠️ Acceso a la Infraestructura

### VPS
- **IP:** 31.97.136.81
- **Puerto SSH:** 22
- **Directorio del proyecto:** `/root/projects/dmc/`

### Bytebot (Instancia DMC)
- **Puerto:** 11000
- **Contenedor Docker:** `dmc-bytebot`
- **URL de acceso:** `http://31.97.136.81:11000`

### Make.com Workflows
Este proyecto tiene 2 workflows configurados:

1. **DMC → Perplexity AI**  
   - Envía consultas a Perplexity para investigación y análisis
   - Webhook URL: _[Ver en Make.com]_

2. **DMC → Bytebot**  
   - Envía instrucciones directas al Bytebot para ejecución
   - Webhook URL: _[Ver en Make.com]_

Accede a los workflows: [Make.com Dashboard](https://us2.make.com/1548754/scenarios)

---

## 📝 Archivos Importantes

### 1. `dmc-state.json`
Almacena el estado actual del proyecto:
```json
{
  \"project\": \"DMC\",
  \"domain\": \"denmicabez.online\",
  \"port\": 11000,
  \"last_update\": \"2025-11-06T10:00:00Z\",
  \"tasks_completed\": [],
  \"tasks_pending\": [],
  \"status\": \"ready\"
}
```

**Ubicación:** `/root/projects/dmc/dmc-state.json`

### 2. `notify.sh`
Script para enviar notificaciones a Telegram:
```bash
#!/bin/bash
MESSAGE=\"$1\"
curl -X POST https://api.telegram.org/bot8392471495:AAEzCZYBsBlNCNXYRhPvuY5oWJoWnv89um8/sendMessage \\
  -d chat_id=TU_CHAT_ID_AQUI \\
  -d text=\"[DMC] $MESSAGE\"
```

**Uso:**
```bash
bash /root/projects/dmc/notify.sh \"Mensaje de prueba\"
```

### 3. `docker-compose.yml`
Configuración del contenedor Bytebot:
```yaml
version: '3.8'
services:
  dmc-bytebot:
    image: bytebot:latest
    container_name: dmc-bytebot
    ports:
      - \"11000:3000\"
    environment:
      - PROJECT_NAME=DMC
      - DOMAIN=denmicabez.online
    restart: always
```

---

## ⚙️ Primeras Tareas

### Tarea 1: Verificar el Estado del Bytebot
```bash
# Conectarse al VPS
ssh root@31.97.136.81

# Verificar que el contenedor está corriendo
docker ps | grep dmc-bytebot

# Ver logs recientes
docker logs --tail 50 dmc-bytebot

# Probar la API
curl http://localhost:11000/health
```

**Resultado esperado:** Estado `200 OK` con respuesta JSON.

---

### Tarea 2: Probar los Workflows de Make.com
1. Accede a [Make.com Dashboard](https://us2.make.com/1548754/scenarios)
2. Busca los workflows de DMC:
   - `DMC - Send to Perplexity`
   - `DMC - Send to Bytebot`
3. Activa ambos workflows (toggle en ON)
4. Ejecuta una prueba manual:
   - Click en \"Run once\"
   - Revisa los logs de ejecución

---

### Tarea 3: Configurar Tu Chat ID de Telegram
1. Abre Telegram y busca el bot: **@IpelVPSbot**
2. Envía el mensaje: `/start`
3. Envía el mensaje: `/mychatid`
4. Copia tu Chat ID
5. Actualiza el archivo `notify.sh`:

```bash
ssh root@31.97.136.81
nano /root/projects/dmc/notify.sh
# Reemplaza TU_CHAT_ID_AQUI con tu ID
```

6. Prueba la notificación:
```bash
bash /root/projects/dmc/notify.sh \"Hola desde DMC\"
```

---

## 🔄 Flujo de Trabajo Diario

1. **Monitoreo Automático**
   - El sistema te notificará vía Telegram de cualquier evento importante
   - No necesitas revisar manualmente el VPS

2. **Revisión del Estado (Opcional - 1 vez al día)**
   ```bash
   cat /root/projects/dmc/dmc-state.json
   ```

3. **Si hay Problemas**
   - Revisa logs: `docker logs dmc-bytebot`
   - Reinicia si es necesario: `docker restart dmc-bytebot`
   - Notifica al equipo via Telegram

---

## 🚨 Troubleshooting

### Problema: Bytebot no responde
```bash
# Ver estado del contenedor
docker ps -a | grep dmc-bytebot

# Si está detenido, reiniciarlo
docker restart dmc-bytebot

# Ver logs para diagnosticar
docker logs --tail 100 dmc-bytebot
```

### Problema: Webhook de Make.com falla
1. Verifica que el puerto 11000 está abierto:
   ```bash
   curl http://31.97.136.81:11000/health
   ```
2. Revisa la URL del webhook en Make.com
3. Comprueba los logs de Make.com para más detalles

### Problema: No llegan notificaciones de Telegram
1. Verifica tu Chat ID en `notify.sh`
2. Prueba manualmente:
   ```bash
   bash /root/projects/dmc/notify.sh \"Test\"
   ```
3. Asegúrate de haber iniciado conversación con @IpelVPSbot

---

## 🔗 Enlaces Útiles

- [Repositorio Principal](https://github.com/jarbelt/ipel-multiproject-docs)
- [Make.com Dashboard](https://us2.make.com/1548754/scenarios)
- [Master Index Gist](https://gist.github.com/jarbelt/b90346979168d0d7b1e1206619e32738)
- [Checkpoint Master](https://gist.github.com/jarbelt/34706d396144bc0be43840dbd2443ff7)

---

## 📞 Contacto

- **Telegram Bot:** @IpelVPSbot
- **Chat Principal:** 5993421355
- **GitHub:** [github.com/jarbelt](https://github.com/jarbelt)

---

**Última actualización:** 06 Noviembre 2025

🚀 **¡Bienvenido al equipo DMC!**
