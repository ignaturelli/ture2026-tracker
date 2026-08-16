# Ture 2026 · Planilla de entrenamiento

PWA de una sola página para anotar entrenos. Sin build, sin framework: todo vive en
[`public/index.html`](public/index.html).

## Cómo funciona

- Cada actividad suma puntos. Las marcadas como *entreno* además cuentan como **una sesión del día**:
  si hacés gimnasio y movilidad el mismo día, son 13 puntos pero **una sola** sesión.
- Los puntos acumulados desbloquean niveles (Arrancando → Leyenda).
- La racha cuenta **semanas** en las que llegaste a la meta de entrenos, no días seguidos.
- La meta anual mide sesiones del año en curso y te dice a qué ritmo semanal tenés que ir.

Para cambiar actividades, puntos, niveles o logros: editá las constantes `ACTIVITIES`,
`LEVELS` y el array `badges` arriba de todo del `<script>`.

## Correr local

```bash
npm run dev     # http://localhost:3002
```

## Datos

Todo se guarda en `localStorage` bajo la key `ture2026_train`:

```json
{ "log": { "2026-08-16": ["gym","mob"] }, "ts": { "2026-08-16": 1755370000000 }, "goals": { "week": 5, "year": 100 } }
```

El sync a Supabase viene **desactivado** (`SB_URL` vacío) y la app funciona igual, solo local.
Para activarlo y ver la misma planilla en el celu y en la compu, seguí las instrucciones del
comentario en la sección `SUPABASE SYNC` del `index.html`.

> La key `ture2026` de localStorage es del tracker de hábitos anterior. No se toca ni se lee,
> queda ahí por si algún día querés recuperar esos datos.

## Recordatorios

[`.github/workflows/reminders.yml`](.github/workflows/reminders.yml) manda mensajes por Telegram
vía cron de GitHub Actions. Usa los secrets `TELEGRAM_TOKEN` y `TELEGRAM_CHAT_ID` del repo.
Se puede probar a mano desde la pestaña Actions con *Run workflow*.

## Deploy

Vercel, sitio estático desde `public/`. Push a `master` y listo.
