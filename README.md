# 📚 Documentación Multi-Proyecto IPEL

**Documentación centralizada para colaboradores de los proyectos IPEL, MIN, DMC y GRM**

Este repositorio contiene todas las guías necesarias para que los colaboradores puedan trabajar de manera autónoma 24/7 sin necesidad de intervención manual.

---

## 🔗 Enlaces Rápidos

### 📋 Guías de Proyectos
- [Guía MIN - minversion.online](./MIN-Colaborador-Guia.md)
- [Guía DMC - denmicabez.online](./DMC-Colaborador-Guia.md)
- [Guía GRM - graciasalriesgodemuerte.com](./GRM-Colaborador-Guia.md)

### 📡 GitHub Gists (Sistema de Continuidad)
- [Master Index](https://gist.github.com/jarbelt/b90346979168d0d7b1e1206619e32738)
- [Checkpoint Master](https://gist.github.com/jarbelt/34706d396144bc0be43840dbd2443ff7)
- [Deploy Script](https://gist.github.com/jarbelt/c9465b5a27876742cedd80ed68a7dc2a)
- [Quick Guide](https://gist.github.com/jarbelt/64282d5d8d6cd2096c64492e44557c60)

---

## 🏗️ Arquitectura del Sistema

### Infraestructura VPS
- **IP:** 31.97.136.81
- **Puertos Asignados:**
  - IPEL: 9999
  - MIN: 10000
  - DMC: 11000
  - GRM: 12000

### Componentes Principales
1. **Bytebot** (4 instancias en Docker)
2. **Make.com** (8 workflows: 2 por proyecto)
3. **Telegram Bot:** IpelVPSbot
4. **PostgreSQL** (base de datos compartida con esquemas separados)

---

## 📝 Estructura de Archivos en VPS

```
/root/projects/
├── ipel/
│   ├── ipel-state.json
│   ├── notify.sh
│   ├── generate-handoff.sh
│   └── docker-compose.yml
├── min/
│   ├── min-state.json
│   ├── notify.sh
│   └── docker-compose.yml
├── dmc/
│   ├── dmc-state.json
│   ├── notify.sh
│   └── docker-compose.yml
└── grm/
    ├── grm-state.json
    ├── notify.sh
    └── docker-compose.yml
```

---

## ⚙️ Flujo de Trabajo Automatizado

```
Usuario/IA Orquestador
    ↓
Make.com Webhook
    ↓
Bytebot (Puerto Específico)
    ↓
Ejecución de Tarea
    ↓
Actualización de state.json
    ↓
Notificación Telegram
    ↓
Continuidad Automática
```

---

## 🛠️ Acceso para Colaboradores

### Para MIN (minversion.online)
Consulta la [Guía completa de MIN](./MIN-Colaborador-Guia.md)

**Primeras tareas:**
1. Verificar estado del Bytebot en puerto 10000
2. Revisar workflows en Make.com
3. Probar notificaciones vía Telegram

### Para DMC (denmicabez.online)
Consulta la [Guía completa de DMC](./DMC-Colaborador-Guia.md)

**Primeras tareas:**
1. Verificar estado del Bytebot en puerto 11000
2. Revisar workflows en Make.com
3. Probar notificaciones vía Telegram

### Para GRM (graciasalriesgodemuerte.com)
Consulta la [Guía completa de GRM](./GRM-Colaborador-Guia.md)

**Primeras tareas:**
1. Verificar estado del Bytebot en puerto 12000
2. Revisar workflows en Make.com
3. Probar notificaciones vía Telegram

---

## 🔄 Sistema de Continuidad

Este sistema garantiza operación 24/7 sin intervención manual:

1. **state.json:** Almacena el estado actual de cada proyecto
2. **handoff.txt:** Protocolo de transferencia entre hilos
3. **GitHub Gists:** Respaldo persistente y sincronización
4. **Telegram:** Notificaciones en tiempo real

### Comandos Útiles en VPS

```bash
# Ver estado de un proyecto
cat /root/projects/min/min-state.json

# Generar handoff manual
bash /root/projects/min/generate-handoff.sh

# Enviar notificación de prueba
bash /root/projects/min/notify.sh "Mensaje de prueba"

# Ver logs de Docker
docker logs min-bytebot
```

---

## 📞 Contacto y Soporte

- **Telegram Bot:** @IpelVPSbot
- **Chat ID Principal:** 5993421355
- **GitHub:** [github.com/jarbelt](https://github.com/jarbelt)

---

## 🚨 Troubleshooting

### Problema: Bytebot no responde
```bash
# Reiniciar contenedor específico
docker restart min-bytebot

# Ver logs
docker logs --tail 50 min-bytebot
```

### Problema: Webhook no funciona
1. Verificar URL del webhook en Make.com
2. Comprobar que el puerto está abierto
3. Revisar logs de Make.com

### Problema: No llegan notificaciones
```bash
# Probar notificación manual
curl -X POST https://api.telegram.org/bot8392471495:AAEzCZYBsBlNCNXYRhPvuY5oWJoWnv89um8/sendMessage \
  -d chat_id=5993421355 \
  -d text="Test"
```

---

## 📊 Estado Actual del Sistema

✅ **IPEL:** Infraestructura configurada, Fase 0 en ejecución  
✅ **MIN:** Listo para inicio de operaciones  
✅ **DMC:** Listo para inicio de operaciones  
✅ **GRM:** Listo para inicio de operaciones  

**Última actualización:** 06 Noviembre 2025, 10:00 AM EST

---

## 🔐 Credenciales y Accesos

> **IMPORTANTE:** Las credenciales sensibles NO se almacenan en este repositorio público.  
> Contacta al administrador para obtener acceso a:
> - Claves SSH del VPS
> - Tokens de Make.com
> - Credenciales de base de datos
> - Variables de entorno

---

🎉 **Bienvenido al equipo multi-proyecto IPEL**  
*Sistema diseñado para operación autónoma 24/7 sin intervención manual*
