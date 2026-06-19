# ddos-tracker

Backend Python para el monitor Anti-DDoS de carlosdev.xyz.

## Endpoints

| Método | Ruta | Descripción |
|--------|------|-------------|
| POST | `/visit` | Registra visita con IP real |
| POST | `/event` | Registra evento de Cloudflare (block/warn/allow) |
| GET | `/stats` | Devuelve estadísticas acumuladas |
| GET | `/health` | Healthcheck |

## Deploy en Railway

1. Subí esta carpeta a un repo de GitHub
2. Entrá a [railway.app](https://railway.app) → New Project → Deploy from GitHub
3. Seleccioná el repo, Railway detecta el `Procfile` solo
4. En Variables de entorno agregá:
   - `DB_PATH` = `ddos.db` (o dejalo vacío, usa ese valor por defecto)
5. Copiá la URL pública que te da Railway (ej: `https://ddos-tracker-production.up.railway.app`)
6. Pegala como `API_URL` en el JS del portafolio

## Ejemplo de uso desde el frontend

```js
// Registrar visita
fetch('https://TU_URL.railway.app/visit', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ ip, country, city, org, is_datacenter })
})

// Obtener stats
const res = await fetch('https://TU_URL.railway.app/stats')
const data = await res.json()
// data.events.blocked → total bloqueadas
// data.events.clean_pct → % tráfico limpio
// data.visits.total → visitas totales
```
