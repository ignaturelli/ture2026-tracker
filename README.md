# Ture 2026 · Planilla de entrenamiento

PWA de una sola página para anotar entrenos. Guarda todo en el propio dispositivo, sin cuentas ni servidores. Sin build, sin framework: todo vive en
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

**No hay servidor ni base de datos.** Todo se guarda en el `localStorage` del dispositivo que
estés usando, bajo la key `ture2026_train`:

```json
{ "log": { "2026-08-16": ["gym","mob"] }, "ts": { "2026-08-16": 1755370000000 }, "goals": { "week": 5, "year": 100 } }
```

Consecuencias, para tenerlas presentes:

- El celu y la compu llevan planillas separadas, cada una con lo suyo.
- Si borrás los datos del navegador o desinstalás la PWA, se pierde lo cargado en ese dispositivo.
- Funciona sin internet.

El puntito arriba a la derecha muestra el estado del guardado: verde *guardado*, amarillo
*guardando*, rojo *no se guardó* (pasa si el navegador está en modo privado o sin espacio).

> La key `ture2026` de localStorage es del tracker de hábitos anterior. No se toca ni se lee,
> queda ahí por si algún día querés recuperar esos datos.

## Deploy

Vercel, sitio estático desde `public/`.

Ojo: la production branch del proyecto en Vercel **no** es `master`, así que un push solo genera
un deployment de Preview y el dominio sigue mostrando lo viejo. Hasta arreglar eso en
Settings > Git, después de pushear hay que promover a mano:

```bash
vercel ls ture2026-tracker        # copiar la URL del preview mas reciente
vercel promote <url> --yes
```
